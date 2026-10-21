
#POWERSHELL 

When a system suddenly bottlenecks and you are already in PowerShell, looking at Get-ScheduledTask is a smart security check, but you can also actively hunt the performance hog in real time.
Here is a targeted blueprint to catch both malicious persistence and resource hogs right now.

🔍 Part 1: Catching the Performance Killer (Real-Time Investigation)

If a task or a process is currently crushing your system, run these commands to isolate it immediately.

1. Find the top CPU/Memory consumers right now

This groups processes and sorts them by what is actually killing your performance.
powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10 -Property Name, CPU, Id, Description
Use code with caution.
(Swap CPU out for WorkingSet64 to sort by RAM usage instead.)

2. Cross-reference Process IDs (PID) with Scheduled Tasks

If a suspicious task is the bottleneck, it will spawn a process. You can map tasks to active processes using this snippet:
powershell
Get-ScheduledTask | Where-Object {$_.State -eq "Running"} | Get-ScheduledTaskInfo | Select-Object TaskName, LastRunTime, LastTaskResult
Use code with caution.

🛡️ Part 2: Filtering Out "Known Good" to Find Suspicious Tasks

Since you are looking for unexpected changes, let's filter out the hundreds of standard Microsoft entries to find third-party or hidden scheduled tasks.

1. Look for Tasks Executing Raw PowerShell or Command Prompt

Attackers (and some messy legacy apps) love running obfuscated scripts or command lines via scheduled tasks. This reveals exactly what script or executable the task is calling:
powershell
Get-ScheduledTask | Where-Object {$_.TaskPath -notlike "\Microsoft*"} | 
    Select-Object TaskName, TaskPath, State, 
    @{N="Executable";E={$_.Actions.Execute}}, 
    @{N="Arguments";E={$_.Actions.Arguments}} | 
    Format-List
Use code with caution.
• What to watch out for: Look at the Arguments field. If you see loops, strings of random characters (Base64), or paths to temporary directories (like AppData\Local\Temp), that is a major red flag.

2. Find Tasks Created or Altered Recently

Since this bottleneck started suddenly, find tasks that registered a change or ran exactly around the time the slowdown began:
powershell
Get-ScheduledTask | Get-ScheduledTaskInfo | 
    Where-Object {$_.LastRunTime -gt (Get-Date).AddDays(-2)} | 
    Sort-Object LastRunTime -Descending | 
    Select-Object TaskName, LastRunTime, LastTaskResult
Use code with caution.

⏱️ Part 3: Deep System Diagnostic

If processes and tasks look normal, the bottleneck might be a disk I/O, network loop, or an unstable driver.

1. Check Disk Queue Length

If your disk usage is pinned at 100%, the CPU will stall waiting for it. If this number is higher than 2, your drive is bottlenecking.
powershell
Get-Counter '\PhysicalDisk(_Total)\Current Disk Queue Length'
Use code with caution.

2. Check Network Connections (Potential Cryptojacker/Exfiltration)

If the bottleneck is paired with high network usage, see what external IPs your local processes are talking to:
powershell
Get-NetTCPConnection | Where-Object {$_.State -eq "Established"} | 
    Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort, OwningProcess | 
    Sort-Object OwningProcess
Use code with caution.
(You can take the OwningProcess ID from this output and run Get-Process -Id <PID> to see exactly what application owns that connection).
What does your Task Manager or the Top 10 CPU process query show as the biggest resource drain right now (e.g., powershell.exe, svchost.exe, a browser, or an unknown .exe)? If you find a specific process ID or a weird task name, paste it here and we can dissect it!

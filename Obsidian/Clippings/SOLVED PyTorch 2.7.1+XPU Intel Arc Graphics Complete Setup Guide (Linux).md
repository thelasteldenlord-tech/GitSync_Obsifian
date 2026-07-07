---
title: "SOLVED: PyTorch 2.7.1+XPU Intel Arc Graphics Complete Setup Guide (Linux)\""
source: "https://discuss.pytorch.org/t/solved-pytorch-2-7-1-xpu-intel-arc-graphics-complete-setup-guide-linux/220821"
author:
  - "[[Innomen]]"
published: 2025-06-14
created: 2026-02-07
description: "Went down a bit of an AI tech support rabbit hole. 10 hours later I thought I’d share the bottom. This is a low effort AI post. Just hoping it saves people some time. This will likely be a drive by XD :white_check_mark: …"
tags:
  - "clippings"
---
## post by Innomen on Jun 14, 2025

[Innomen](https://discuss.pytorch.org/u/innomen)

[Jun 2025](https://discuss.pytorch.org/t/solved-pytorch-2-7-1-xpu-intel-arc-graphics-complete-setup-guide-linux/220821 "Post date")

Went down a bit of an AI tech support rabbit hole. 10 hours later I thought I’d share the bottom. This is a low effort AI post. Just hoping it saves people some time. This will likely be a drive by XD

## SOLVED: PyTorch 2.7.1+XPU on Intel Arc Graphics - Complete Setup Guide

## SUCCESS! PyTorch XPU Working on Intel Arc Graphics

After extensive troubleshooting, I’ve successfully got PyTorch XPU working with Intel Arc Graphics on Linux. Sharing the complete solution to help others facing similar issues.

**Quick Verification:**

```python
import torch
print(f"PyTorch version: {torch.__version__}")
print(f"XPU compiled: {torch._C._xpu_getDeviceCount is not None}")
print(f"XPU available: {torch.xpu.is_available()}")
print(f"Device count: {torch.xpu.device_count()}")
print(f"Device name: {torch.xpu.get_device_name(0)}")

# Test tensor creation
x = torch.randn(3, 3, device='xpu')
print(f"Test tensor: {x.size()} {x.device}")
```

**Output:**

```python
PyTorch version: 2.7.1+xpu
XPU compiled: True
XPU available: True
Device count: 1
Device name: Intel(R) Arc(TM) Graphics
Test tensor: torch.Size([3, 3]) xpu:0
```

## Working Installation Command

The solution that worked after 8 full conversations of iterations of troubleshooting: Approx 10 hours. (Point and laugh if you must, I am 6 months into my 100% Linux daily driver journey XD)

```bash
# IMPORTANT: Complete clean uninstall first
pip uninstall -y torch torchvision torchaudio intel-cmplr-lib-rt intel-cmplr-lib-ur intel-cmplr-lic-rt intel-sycl-rt pytorch-triton-xpu tcmlib umf intel-pti

# Fresh install with all Intel runtime dependencies
pip install torch==2.7.1+xpu torchvision==0.22.1+xpu torchaudio==2.7.1+xpu intel-cmplr-lib-rt intel-cmplr-lib-ur intel-cmplr-lic-rt intel-sycl-rt pytorch-triton-xpu tcmlib umf intel-pti --index-url https://download.pytorch.org/whl/xpu --extra-index-url https://pypi.org/simple
```

## Key Breakthrough Discovery

**The Root Cause**: Partial installations and version mixing between system packages and pip packages caused library path conflicts.

**The Solution**: Complete clean slate reinstallation of the entire PyTorch XPU + Intel runtime stack.

## System Specifications

- **Hardware**: Intel Meteor Lake-P with integrated Arc Graphics
- **OS**: Arch Linux (kernel 6.x)
- **Python**: 3.11.6 via pyenv
- **GPU**: Intel Arc Graphics (128 compute units)
- **Driver**: i915 with GuC/HuC firmware

## Prerequisites

1. **System Level Zero** (install via package manager):
	```bash
	# Arch Linux
	sudo pacman -S level-zero-loader level-zero-headers
	# Ubuntu/Debian
	sudo apt install level-zero level-zero-dev
	```
2. **Intel Compute Runtime** (should be installed automatically with modern kernels)
3. **Verify GPU Detection**:
	```bash
	ls /dev/dri/  # Should show renderD128 or similar
	clinfo        # Should list Intel GPU (if OpenCL tools installed)
	```

## Critical Success Factors

### 1\. Use PyTorch 2.7.1+xpu (Not IPEX)

- PyTorch 2.7.1+xpu has **native Intel GPU support**
- No need for Intel Extension for PyTorch (IPEX)
- XPU backend is built-in

### 2\. Install ALL Intel Runtime Dependencies

The pip command above installs these essential Intel 2025.0.4 runtime components:

- `intel-cmplr-lib-rt-2025.0.4`
- `intel-cmplr-lib-ur-2025.0.4`
- `intel-cmplr-lic-rt-2025.0.4`
- `intel-sycl-rt-2025.0.4`
- `pytorch-triton-xpu-3.3.1`

### 3\. Clean Slate Installation

- Don’t try to update existing installations
- Uninstall everything PyTorch and Intel-related first
- Fresh installation resolves library conflicts

## Common Issues & Solutions

### Issue: “XPU is not available”

**Solution**: Make sure you installed from the XPU index URL and included all Intel runtime dependencies.

### Issue: Segmentation faults or crashes

**Solution**: Version conflicts between system and pip packages. Do complete uninstall/reinstall.

### Issue: ImportError for Intel libraries

**Solution**: Install all Intel runtime dependencies listed in the command above.

### Issue: Level Zero version warnings

**Note**: Version mismatch warnings between PyTorch expectations and system Level Zero are usually non-critical if basic tensor operations work.

## Validation Steps

After installation, verify everything works:

```python
import torch

# Basic checks
assert torch.xpu.is_available(), "XPU not available"
assert torch.xpu.device_count() > 0, "No XPU devices found"

# Create and operate on XPU tensor
x = torch.randn(1000, 1000, device='xpu')
y = torch.randn(1000, 1000, device='xpu')
z = torch.mm(x, y)  # Matrix multiplication on GPU

print(f"✅ Success! Tensor device: {z.device}")
print(f"✅ GPU: {torch.xpu.get_device_name(0)}")
```

## What This Enables

With working PyTorch XPU, you can now:

- Train neural networks on Intel GPU
- Accelerate tensor computations
- Use Intel Arc Graphics for AI workloads
- Develop with native PyTorch GPU support

## Complete Documentation

I’ve documented the entire troubleshooting journey with technical details, failed attempts, and system configuration info. The full technical report includes:

- 8 iteration attempts with detailed failure analysis
- Dependency conflict resolution
- Fish shell compatibility notes
- Performance validation steps

## Help Others

If this helped you, please:

- Share your success in replies
- Note any variations for your system
- Report any issues you encounter

## Tags

#intel-gpu #xpu #arc-graphics #pytorch-installation #linux #gpu-acceleration #intel-arc

## post by Innomen on Jun 15, 2025

8 days later

## post by VladD on Jun 24, 2025

## post by Innomen on Jun 24, 2025

## post by DrThodt2021 on Jun 30, 2025

## post by Innomen on Jul 1, 2025

## post by Innomen on Jul 2, 2025

## post by DrThodt2021 on Jul 2, 2025

6 months later

## post by Barry\_Yang on Dec 15, 2025

## post by Innomen on Dec 15, 2025

## post by Jonas1 on Dec 15, 2025

## post by Innomen on Dec 15, 2025

## post by Jonas1 on Dec 15, 2025

## post by FredZeFenec on Dec 17, 2025

10 days later

## post by FredZeFenec on Dec 28, 2025

  

[Powered by Discourse](https://discourse.org/powered-by)
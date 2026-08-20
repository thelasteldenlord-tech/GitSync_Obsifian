To apply custom the ring simply replace the values in the file and reload the config file located in the home directory, usually:
``` bash

# Edit the Termux colors file, adding the theme colors from below or use the script to do it automatically
nano ~/.termux/colors.properties

```

# Cyberpunk Colors
# Primary Terminal UI Configuration
background=#0d0e12
foreground=#e1e4ed
cursor=#ff0055

# 16 Standard ANSI Colors (Used by Oh My Zsh and CLI apps)
---
``` bash
# All colors use a dark and a light shade, dark is the first color. Light follows on the next line as seen in black"
#
# Black (Dark)
color0=#16171f
# Black (Dark)
color8=#2b2d3d
# Red
color1=#ff4a6b
color9=#ff6b8b
# Green (Perfect for status checks)
color2=#00e699
color10=#33ffbb
# Yellow
color3=#e6b800
color11=#ffd633
# Blue (Often used for main prompt backgrounds)
color4=#66b2ff
color12=#99ccff
# Magenta
color5=#9b51e0
color13=#b57bed
# Cyan
color6=#00f0ff
color14=#55f7ff
# White
color7=#a9b2c3
color15=#ffffff
Termux uses a colors. Properties file to color the terminal, can you generate a custom dark theme with a dark charcoal by then using oranges and yellows for the base16 colors theme colors in base16 using the same format? An example theme is (each on a new line): 
```

# Copy and paste into a new file and run the command ./theme.sh

``` bash
mkdir -p ~/.bash_scripts/
```
background=#0d0e12 
foreground=#e1e4ed
cursor=#ff0055, 

# 0-15 (16 Standard ANSI Colors)
color0=#16171f
color1=#ff4a6b
color2=#00e699
color3=#e6b800
color4=#66b2ff
color5=#9b51e0
color6=#00f0ff
color7=#a9b2c3
color8=#2b2d3d
color9=#ff6b8b
color10=#33ffbb
color11=#ffd633
color12=#99ccff
color13=#b57bed
color14=#55f7ff
color15=#ffffff

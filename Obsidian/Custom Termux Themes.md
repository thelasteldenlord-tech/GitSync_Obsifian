To apply custom the ring simply replace the values in the file and reload the config file located in the home directory, usually:
``` bash


```

# Cyberpunk Colors
# Primary Terminal UI Configuration

# 16 Standard ANSI Colors (Used by Oh My Zsh and CLI apps)
---
``` bash

# Theme: "Cybergrr"; Author: Daniel Moore
# I made for personal use, use with caution. If you'd like to comment or communicate,
# you can always Email me at daniel@swvaclean.com
#`And be patient, I respond slowly

# All colors use a dark and a light shade, dark is the 
# first color. Light follows on the next line as seen in black"

# Create theme installer directory, please ensure this doesn't overwrite anything
CREATE_SCRIPT_DIR=mkdir~ -p ~/.bash_scripts/daniels_termux_theme_installers/



# Create bash script for this themes installer
touch ~/.bash_scripts/daniels_termux_theme_installers/cyber.sh



# Edit the Termux colors file, adding the theme colors from below or use the script to do it automatically
nano ~/.termux/colors.properties


# Main elements
background=#0d0e12
foreground=#e1e4ed
cursor=#ff0055

# Black (Dark, color0) / Black (Lighter, 'color8')
color0=#16171f
color8=#2b2d3d

# Red
color1=#ff4a6b
color9=#ff6b8b

# Green
color2=#00e699
color10=#33ffbb

# Yellow
color3=#e6b800
color11=#ffd633

# Blue
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

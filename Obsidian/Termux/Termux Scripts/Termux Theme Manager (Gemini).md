
---
```bash

#!/bin/bash
# TERMUX COLOR THEME MANAGER SCRIPT
# Author: Gemini (Gemma 4 via LMStudio)

# Description: Provides a 
# safe, menu-driven way
# to backup and restore the 
# ~/.termux.colors.properties file.
COLOR_FILE="$HOME/.termux.colors.properties"
BACKUP_FILE="${COLOR_FILE}.bak"
# --- Function Definitions ---
# Function to display a friendly welcome 
# message and instructions

display_welcome() {

    echo "====================================================="

    echo "✨ Welcome to the Termux Theme Manager! ✨"

    echo "This script helps you safely backup and restore your custom colors."

    echo "-----------------------------------------------------"

    echo "Target File: $COLOR_FILE"

    echo "Backup File: $BACKUP_FILE"

    echo "====================================================="

}

  

# Function to check if the target file exists

check_file() {

    if [ ! -f "$COLOR_FILE" ]; then

        echo ""

        echo "WARNING: The color properties file ($COLOR_FILE) does not exist."

        echo "Please create it first, or run option 1 to initialize a new theme."

        return 1

    fi

}

  

# Function to perform the backup operation

backup_theme() {

    if [ -f "$BACKUP_FILE" ]; then

        echo ""

        echo "Backup already exists! You can restore it using Option 2."

        return

    fi

  

    echo ""

    echo " --- BACKUP OPERATION STARTED ---"

    echo "Creating backup file: $BACKUP_FILE..."

    cp "$COLOR_FILE" "$BACKUP_FILE"

  

    if [ $? -eq 0 ]; then

        echo "SUCCESS! Backup created successfully."

        echo "You can now restore this theme if needed (Option 2)."

    else

        echo "ERROR: Failed to create the backup file. Check permissions."

    fi

}

  

# Function to perform the restore operation

restore_theme() {

    if [ ! -f "$BACKUP_FILE" ]; then

        echo ""

        echo "🚨 ERROR: Backup file ($BACKUP_FILE) not found!"

        echo "Please run Option 1 first to create a backup before restoring."

        return

    fi

  

    echo ""

    echo "🔄 --- RESTORE OPERATION STARTED ---"

    echo "Restoring theme from $BACKUP_FILE to $COLOR_FILE..."

    cp "$BACKUP_FILE" "$COLOR_FILE"

  

    if [ $? -eq 0 ]; then

        echo "🎉 SUCCESS! Theme restored successfully."

        echo "Please restart Termux or reload your configuration for changes to take effect."

    else

        echo "❌ ERROR: Failed to restore the theme. Check permissions."

    fi

}

  

# Function to initialize a new file (for beginners)

initialize_theme() {

    echo ""

    echo "🆕 --- INITIALIZATION OPERATION STARTED ---"

    echo "Creating a basic, safe template for $COLOR_FILE..."

    cat << EOF > "$COLOR_FILE"

# ==============================================================================

# Custom Termux Color Theme Configuration File

# Created by Theme Manager Script on $(date)

# ==============================================================================

  

# --- BASE 16 COLORS (For custom UI elements, use these values!) ---

color0=#21222c  # Example: Dark background color for the main terminal area

color1=#3a3b45  # Example: Slightly lighter element color

color2=#1e88e5  # Example: Bright accent color (Blue)

color3=#ffeb3b  # Example: Warning/Highlight color (Yellow)

color4=#f44336  # Example: Error color (Red)

color5=#4caf50  # Example: Success color (Green)

color6=#9c27b0  # Example: Purple accent

  

# --- TERMINAL SETTINGS (Use these for overall terminal appearance) ---

background=color0   # Sets the main background color of the terminal window.

foreground=color1    # Sets the default text color.

cursor=color3        # Sets the color of the blinking cursor.
```bash

#!/bin/bash

# Advanced OSINT Toolkit for Termux
# Version 1.0


# Color Codes for Enhanced Readability
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
NC='\033[0m' # No Color

# Dependency Check Function
check_dependencies() {
    echo -e "${BLUE}[*] Checking required dependencies...${NC}"
    
    # List of required tools
    DEPENDENCIES=(
        "pip" "git" "curl" "wget" "nmap" "whois" 
        "traceroute" "dnsutils" "metagoofil" "theHarvester"
    )
    
    for tool in "${DEPENDENCIES[@]}"; do
        if ! command -v "$tool" &> /dev/null; then
            echo -e "${YELLOW}[!] Installing $tool...${NC}"
            pkg install -y "$tool"
        else
            echo -e "${GREEN}[✓] $tool is installed${NC}"
        fi
    done

    # Python-based OSINT tools
    pip install --upgrade \
        shodan \
        censys \
        networkx \
        holehe \
        pwnedpasswords \
        spyse-python
}

# Main Menu Function
display_main_menu() {
    clear
    echo -e "${BLUE}===== 🕵️ Claude's OSINT Toolkit 🕵️ =====${NC}"
    echo -e "${GREEN}1.  🌐 Domain Reconnaissance${NC}"
    echo -e "${GREEN}2.  🔍 IP/Network Intelligence${NC}"
    echo -e "${GREEN}3.  📧 Email OSINT${NC}"
    echo -e "${GREEN}4.  👤 Username Investigation${NC}"
    echo -e "${GREEN}5.  🌐 Web Footprinting${NC}"
    echo -e "${GREEN}6.  📦 Metadata Extraction${NC}"
    echo -e "${GREEN}7.  📚 OSINT Learning Resources${NC}"
    echo -e "${GREEN}8.  🛠️ Update Toolkit${NC}"
    echo -e "${GREEN}9.  ❌ Exit${NC}"
    echo -e "${BLUE}========================================${NC}"
}

# Domain Reconnaissance Function
domain_recon() {
    read -p "Enter domain to investigate: " domain
    
    echo -e "${YELLOW}[*] Performing Comprehensive Domain Reconnaissance${NC}"
    
    # Multiple reconnaissance techniques
    whois "$domain"
    echo -e "\n${BLUE}[*] DNS Enumeration:${NC}"
    dig +short "$domain"
    
    # TheHarvester for email and subdomain discovery
    theHarvester -d "$domain" -l 500 -b all
}

# IP/Network Intelligence Function
ip_intelligence() {
    read -p "Enter IP or network range: " ip_target
    
    echo -e "${YELLOW}[*] Network Vulnerability Assessment${NC}"
    nmap -sV -sC "$ip_target"
    
    # Geolocation and threat intelligence
    curl "https://ipapi.co/$ip_target/json/"
}

# Email OSINT Function
email_osint() {
    read -p "Enter email address: " email
    
    # Multiple email investigation techniques
    holehe "$email"
    
    # Check for data breaches
    pwnedpasswords "$email"
}

# Username Investigation Function
username_investigation() {
    read -p "Enter username: " username
    
    echo -e "${YELLOW}[*] Cross-Platform Username Search${NC}"
    # Sherlock for username investigation
    sherlock "$username"
}

# Metadata Extraction
metadata_extraction() {
    read -p "Enter file path: " file_path
    
    # Metagoofil for metadata analysis
    metagoofil -d "$domain" -t all -o ./metadata_output
}

# OSINT Learning Resources
osint_resources() {
    echo -e "${BLUE}🌟 OSINT Learning Resources 🌟${NC}"
    echo -e "${GREEN}Online Platforms:${NC}"
    echo "1. OSINT Framework: https://osintframework.com/"
    echo "2. SANS OSINT Cheat Sheet: https://www.sans.org/posters/osint/"
    
    echo -e "\n${GREEN}Educational Websites:${NC}"
    echo "1. IntelTechniques: https://inteltechniques.com/"
    echo "2. OSINT Curious: https://osintcurio.us/"
    
    echo -e "\n${GREEN}YouTube Channels:${NC}"
    echo "1. OSINT Dojo"
    echo "2. NetworkChuck OSINT Series"
}

# Main Execution
main() {
    check_dependencies
    
    while true; do
        display_main_menu
        read -p "Select an option (1-9): " choice
        
        case $choice in
            1) domain_recon ;;
            2) ip_intelligence ;;
            3) email_osint ;;
            4) username_investigation ;;
            5) web_footprinting ;;
            6) metadata_extraction ;;
            7) osint_resources ;;
            8) check_dependencies ;;
            9) exit 0 ;;
            *) echo -e "${RED}Invalid option. Try again.${NC}" ;;
        esac
        
        read -p "Press Enter to continue..." pause
    done
}

# Run the main function
main
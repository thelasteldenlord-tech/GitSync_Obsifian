---
title: Bash, Setup Fileserver
updated: 2025-09-02 07:39:38Z
created: 2025-12-19 07:39:06Z
tags:
  - "#homelab"
  - "#bash"
  - "#server"
  - "#localhost"
  - "#daniels-projects"
  - "#claude-code"
  - "#completed"
aliases:
  - home-server files access
reason: Local file availability
status: complete
agent: claude-code
type: personal
---

``` bash
#!/bin/bash

# Media Server Directory Structure Generator
# Creates comprehensive directory structure for books, games, apps, and user content
# Usage: ./setup_media_server.sh [base_path]

set -euo pipefail

# Configuration
BASE_PATH="${1:-/var/www/html/lan}"
NGINX_USER="${NGINX_USER:-www-data}"
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"

# Colors for output
readonly RED='\033[0;31m'
readonly GREEN='\033[0;32m'
readonly YELLOW='\033[1;33m'
readonly BLUE='\033[0;34m'
readonly PURPLE='\033[0;35m'
readonly CYAN='\033[0;36m'
readonly NC='\033[0m' # No Color

# Logging functions
log_info() { echo -e "${BLUE}[INFO]${NC} $1"; }
log_success() { echo -e "${GREEN}[SUCCESS]${NC} $1"; }
log_warning() { echo -e "${YELLOW}[WARNING]${NC} $1"; }
log_error() { echo -e "${RED}[ERROR]${NC} $1"; }

# Directory structure arrays using brace expansion concepts
declare -A BOOK_CATEGORIES=(
    ["fiction"]="sci-fi fantasy mystery thriller romance historical literary young-adult"
    ["non-fiction"]="biography history science technology philosophy self-help health cooking"
    ["reference"]="dictionaries encyclopedias manuals guides textbooks"
    ["audiobooks"]="fiction non-fiction podcasts lectures"
    ["magazines"]="tech science lifestyle gaming retro-computing"
    ["comics"]="marvel dc indie manga webcomics"
    ["archives"]="rare out-of-print classics vintage"
)

declare -A GAME_CATEGORIES=(
    ["consoles"]="nintendo sega sony microsoft atari neo-geo"
    ["handhelds"]="gameboy nintendo-ds psp vita"
    ["arcade"]="mame neo-geo capcom snk"
    ["computers"]="dos windows mac linux commodore amiga atari-st"
    ["mobile"]="android ios java"
    ["homebrew"]="indie fan-made demos prototypes"
    ["tools"]="emulators frontends save-states cheats"
    ["firmware"]="bios system-files updates"
)

declare -A APP_CATEGORIES=(
    ["productivity"]="office text-editors calculators calendars"
    ["development"]="ides compilers debuggers utilities"
    ["multimedia"]="audio video graphics design"
    ["games"]="strategy puzzle action simulation"
    ["utilities"]="system network security backup"
    ["vintage"]="dos win31 win95 mac-classic"
    ["mobile"]="android apk ios-backups"
    ["source"]="open-source projects libraries frameworks"
)

declare -A USER_CATEGORIES=(
    ["personal"]="documents photos videos music"
    ["shared"]="family-photos group-projects presentations"
    ["backups"]="system-backups app-data user-profiles"
    ["uploads"]="incoming temp-files user-submissions"
    ["archives"]="old-files deprecated legacy"
    ["templates"]="document-templates project-starters"
)

# Console/Platform specific subdirectories
declare -A CONSOLE_DIRS=(
    ["nintendo"]="nes snes n64 gamecube wii wii-u switch"
    ["sega"]="master-system genesis saturn dreamcast game-gear"
    ["sony"]="ps1 ps2 ps3 ps4 ps5 psp vita"
    ["microsoft"]="xbox xbox-360 xbox-one xbox-series"
    ["atari"]="2600 5200 7800 lynx jaguar"
    ["neo-geo"]="aes mvs cd pocket"
)

# File type associations
declare -A FILE_TYPES=(
    ["books"]="pdf epub mobi azw3 djvu txt rtf"
    ["audiobooks"]="mp3 m4a m4b aac flac ogg"
    ["roms"]="rom bin iso img cue gdi chd"
    ["firmware"]="bin rom bios sys"
    ["apps"]="exe msi deb rpm dmg app apk"
    ["docs"]="pdf doc docx txt md rst"
    ["media"]="mp4 mkv avi mov mp3 flac jpg png"
)

# Price/Quality categories for organization
declare -A PRICE_TIERS=(
    ["premium"]="aaa-titles bestsellers professional commercial"
    ["standard"]="indie mid-tier popular mainstream"
    ["budget"]="freeware shareware open-source public-domain"
    ["vintage"]="retro classic legacy historical"
    ["experimental"]="beta alpha prototype demo"
)

create_directory_structure() {
    log_info "Creating base directory structure at $BASE_PATH"
    
    # Create main directories
    mkdir -p "$BASE_PATH"/{books,games,apps,users,archives,tools,docs}
    
    # Books directory structure
    log_info "Setting up books directory structure..."
    for category in "${!BOOK_CATEGORIES[@]}"; do
        mkdir -p "$BASE_PATH/books/$category"
        
        # Create subcategories
        for subcategory in ${BOOK_CATEGORIES[$category]}; do
            mkdir -p "$BASE_PATH/books/$category/$subcategory"
            
            # Create quality/source subdirs
            for tier in "${!PRICE_TIERS[@]}"; do
                mkdir -p "$BASE_PATH/books/$category/$subcategory/$tier"
            done
        done
    done
    
    # Special audiobook structure
    mkdir -p "$BASE_PATH/books/audiobooks"/{complete,series,standalone,collections}
    mkdir -p "$BASE_PATH/books/audiobooks/quality"/{high,standard,compressed}
    
    # Games directory structure
    log_info "Setting up games directory structure..."
    for category in "${!GAME_CATEGORIES[@]}"; do
        mkdir -p "$BASE_PATH/games/$category"
        
        if [[ "$category" == "consoles" ]]; then
            # Create console-specific directories
            for console in "${!CONSOLE_DIRS[@]}"; do
                mkdir -p "$BASE_PATH/games/consoles/$console"
                for system in ${CONSOLE_DIRS[$console]}; do
                    mkdir -p "$BASE_PATH/games/consoles/$console/$system"/{roms,saves,cheats,manuals,artwork}
                    
                    # Region subdirectories
                    mkdir -p "$BASE_PATH/games/consoles/$console/$system/roms"/{usa,europe,japan,other}
                done
            done
        else
            # Create subcategories for other game types
            for subcategory in ${GAME_CATEGORIES[$category]}; do
                mkdir -p "$BASE_PATH/games/$category/$subcategory"
                mkdir -p "$BASE_PATH/games/$category/$subcategory"/{complete,partial,patches}
            done
        fi
    done
    
    # Emulator and tools structure
    mkdir -p "$BASE_PATH/games/tools"/{emulators,frontends,utilities}
    mkdir -p "$BASE_PATH/games/tools/emulators"/{windows,linux,mac,android}
    mkdir -p "$BASE_PATH/games/firmware"/{bios,system-roms,updates}
    
    # Apps directory structure
    log_info "Setting up applications directory structure..."
    for category in "${!APP_CATEGORIES[@]}"; do
        mkdir -p "$BASE_PATH/apps/$category"
        
        for subcategory in ${APP_CATEGORIES[$category]}; do
            mkdir -p "$BASE_PATH/apps/$category/$subcategory"
            
            # Platform-specific subdirs
            mkdir -p "$BASE_PATH/apps/$category/$subcategory"/{windows,linux,mac,cross-platform}
            
            # Version and license subdirs
            mkdir -p "$BASE_PATH/apps/$category/$subcategory"/{current,legacy,portable,source}
        done
    done
    
    # Users directory structure
    log_info "Setting up users directory structure..."
    for category in "${!USER_CATEGORIES[@]}"; do
        mkdir -p "$BASE_PATH/users/$category"
        
        for subcategory in ${USER_CATEGORIES[$category]}; do
            mkdir -p "$BASE_PATH/users/$category/$subcategory"
        done
    done
    
    # Create user-specific directories
    mkdir -p "$BASE_PATH/users/profiles"/{admin,family,guests}
    mkdir -p "$BASE_PATH/users/shared"/{inbox,outbox,collaborative}
    
    # Archives directory structure
    log_info "Setting up archives directory structure..."
    mkdir -p "$BASE_PATH/archives"/{complete-sets,curated-collections,historical,rare}
    mkdir -p "$BASE_PATH/archives/complete-sets"/{console-libraries,software-suites,book-series}
    mkdir -p "$BASE_PATH/archives/preservation"/{original-media,disk-images,documentation}
    
    # Tools and utilities
    log_info "Setting up tools directory structure..."
    mkdir -p "$BASE_PATH/tools"/{converters,extractors,organizers,validators}
    mkdir -p "$BASE_PATH/tools/scripts"/{batch-processing,maintenance,backup}
    
    # Documentation
    mkdir -p "$BASE_PATH/docs"/{manuals,guides,readme-files,licenses}
    mkdir -p "$BASE_PATH/docs/system"/{nginx-config,maintenance-logs,user-guides}
}

create_sample_files() {
    log_info "Creating sample files and README documents..."
    
    # Create README files for major categories
    cat > "$BASE_PATH/README.md" << 'EOF'
# Family Media Server

Welcome to the family media server! This directory contains our shared collection of:

- **Books**: Digital books, audiobooks, and reference materials
- **Games**: Retro games, ROMs, and emulators
- **Apps**: Useful software and utilities
- **Users**: Personal and shared user content
- **Archives**: Complete collections and preserved content
- **Tools**: Utilities for managing and organizing content

## Usage Guidelines

1. Please organize content in the appropriate directories
2. Use descriptive filenames
3. Include README files for new collections
4. Respect copyright and fair use guidelines
5. Keep personal content in user-specific folders

## Directory Structure

Each category is organized by type, quality, and platform for easy navigation.
Use the web interface to browse and download content easily.

Last updated: $(date)
EOF

    # Create category-specific README files
    for category in books games apps users archives; do
        cat > "$BASE_PATH/$category/README.md" << EOF
# ${category^} Directory

This directory contains organized ${category} content for the family media server.

## Organization

Content is organized by:
- Category/Genre
- Quality/Tier
- Platform (where applicable)
- Region (for games)

## Guidelines

- Place content in the most specific appropriate subdirectory
- Use clear, descriptive filenames
- Include source information when possible
- Maintain consistent organization

Created: $(date)
EOF
    done
    
    # Create .htaccess files for better nginx serving
    cat > "$BASE_PATH/.htaccess" << 'EOF'
# Media Server Configuration
Options +Indexes
IndexOptions +FancyIndexing +HTMLTable +SuppressDescription
IndexIgnore README* .htaccess .git*

# Security headers
Header always set X-Content-Type-Options nosniff
Header always set X-Frame-Options DENY
Header always set X-XSS-Protection "1; mode=block"

# Cache static content
<FilesMatch "\.(pdf|epub|mp3|mp4|mkv|avi|zip|rar|7z)$">
    Header set Cache-Control "public, max-age=31536000"
</FilesMatch>
EOF

    # Create nginx-specific index files
    cat > "$BASE_PATH/index.html" << 'EOF'
<!DOCTYPE html>
<html>
<head>
    <title>Family Media Server</title>
    <meta http-equiv="refresh" content="0; url=server.html">
</head>
<body>
    <p>Redirecting to media server interface...</p>
</body>
</html>
EOF
}

set_permissions() {
    log_info "Setting appropriate permissions..."
    
    # Set directory permissions
    find "$BASE_PATH" -type d -exec chmod 755 {} \;
    
    # Set file permissions
    find "$BASE_PATH" -type f -exec chmod 644 {} \;
    
    # Set ownership to nginx user if running as root
    if [[ $EUID -eq 0 ]]; then
        chown -R "$NGINX_USER:$NGINX_USER" "$BASE_PATH"
        log_success "Ownership set to $NGINX_USER"
    else
        log_warning "Not running as root - permissions may need manual adjustment"
    fi
}

create_maintenance_scripts() {
    log_info "Creating maintenance scripts..."
    
    mkdir -p "$BASE_PATH/tools/scripts"
    
    # Directory cleanup script
    cat > "$BASE_PATH/tools/scripts/cleanup.sh" << 'EOF'
#!/bin/bash
# Cleanup script for media server
find /var/www/html/lan -name "*.tmp" -delete
find /var/www/html/lan -name "Thumbs.db" -delete
find /var/www/html/lan -name ".DS_Store" -delete
find /var/www/html/lan -empty -type d -delete 2>/dev/null || true
echo "Cleanup completed at $(date)"
EOF

    # Update script for file listings
    cat > "$BASE_PATH/tools/scripts/update_listings.sh" << 'EOF'
#!/bin/bash
# Update file listings for web interface
BASE_DIR="/var/www/html/lan"
find "$BASE_DIR" -name "*.json" -delete
# Add your file indexing logic here
echo "Listings updated at $(date)"
EOF

    # Make scripts executable
    chmod +x "$BASE_PATH/tools/scripts"/*.sh
}

generate_nginx_config() {
    log_info "Generating nginx configuration..."
    
    cat > "$BASE_PATH/docs/system/nginx-media-server.conf" << EOF
# Nginx configuration for media server
server {
    listen 80;
    server_name media.local lan.local;
    root $BASE_PATH;
    index server.html index.html;
    
    # Security headers
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    
    # Main interface
    location / {
        try_files \$uri \$uri/ =404;
    }
    
    # API endpoint for file listings (implement as needed)
    location /api/ {
        # Add your API logic here
        return 404;
    }
    
    # Static file serving with caching
    location ~* \.(pdf|epub|mobi|mp3|mp4|mkv|avi|zip|rar|7z|rom|iso)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
        add_header Content-Disposition "attachment";
    }
    
    # Directory browsing for specific paths
    location /browse/ {
        alias $BASE_PATH/;
        autoindex on;
        autoindex_exact_size off;
        autoindex_localtime on;
        autoindex_format html;
    }
    
    # Deny access to system files
    location ~ /\. {
        deny all;
    }
    
    location ~ ~$ {
        deny all;
    }
}
EOF

    log_success "Nginx config created at $BASE_PATH/docs/system/nginx-media-server.conf"
    log_info "To enable: sudo ln -s $BASE_PATH/docs/system/nginx-media-server.conf /etc/nginx/sites-available/"
    log_info "Then: sudo nginx -t && sudo systemctl reload nginx"
}

show_completion_summary() {
    log_success "Media server directory structure created successfully!"
    echo
    echo -e "${CYAN}Summary:${NC}"
    echo "📁 Base path: $BASE_PATH"
    echo "🎯 Total directories created: $(find "$BASE_PATH" -type d | wc -l)"
    echo "📄 Documentation files: $(find "$BASE_PATH" -name "README*" | wc -l)"
    echo "🔧 Maintenance scripts: $(find "$BASE_PATH/tools/scripts" -name "*.sh" 2>/dev/null | wc -l)"
    echo
    echo -e "${YELLOW}Next steps:${NC}"
    echo "1. Copy your media files to the appropriate directories"
    echo "2. Configure nginx using the provided config file"
    echo "3. Set up the web interface (server.html)"
    echo "4. Run maintenance scripts as needed"
    echo
    echo -e "${PURPLE}Directory highlights:${NC}"
    echo "📚 Books: Fiction, non-fiction, audiobooks, references"
    echo "🎮 Games: Console ROMs, emulators, firmware, tools"
    echo "💻 Apps: Platform-specific software and utilities"
    echo "👥 Users: Personal and shared content areas"
    echo "📦 Archives: Complete collections and preserved content"
    echo
    echo -e "${GREEN}Happy organizing! 🎉${NC}"
}

main() {
    echo -e "${PURPLE}Media Server Directory Structure Generator${NC}"
    echo "================================================"
    echo
    
    # Validate input
    if [[ ! -d "$(dirname "$BASE_PATH")" ]]; then
        log_error "Parent directory doesn't exist: $(dirname "$BASE_PATH")"
        exit 1
    fi
    
    # Create the structure
    create_directory_structure
    create_sample_files
    set_permissions
    create_maintenance_scripts
    generate_nginx_config
    show_completion_summary
}

# Run main function
main "$@"
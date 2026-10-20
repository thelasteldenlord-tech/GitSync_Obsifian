# URL to Markdown
```python

#!/usr/bin/env python3
"""
Web to Markdown Converter
A simple CLI tool to fetch web pages and convert them to clean Markdown files.
"""

import requests
from bs4 import BeautifulSoup
import html2text
import os
import sys
from urllib.parse import urlparse, urljoin
import re
from pathlib import Path
import time

class WebToMarkdown:
    def __init__(self, output_dir="./markdown"):
        self.output_dir = Path(output_dir)
        self.output_dir.mkdir(exist_ok=True)
        
        # Configure html2text for better output
        self.h = html2text.HTML2Text()
        self.h.ignore_links = False
        self.h.ignore_images = False
        self.h.ignore_emphasis = False
        self.h.body_width = 0  # Don't wrap lines
        self.h.protect_links = True
        self.h.mark_code = True
        self.h.wrap_links = False
        
        # Common headers to appear more like a real browser
        self.headers = {
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36',
            'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8',
            'Accept-Language': 'en-US,en;q=0.5',
            'Accept-Encoding': 'gzip, deflate',
            'DNT': '1',
            'Connection': 'keep-alive',
            'Upgrade-Insecure-Requests': '1',
        }

    def clean_filename(self, filename):
        """Clean filename to be filesystem safe"""
        # Remove or replace invalid characters
        filename = re.sub(r'[<>:"/\\|?*]', '-', filename)
        # Remove multiple dashes
        filename = re.sub(r'-+', '-', filename)
        # Remove leading/trailing dashes and spaces
        filename = filename.strip('- ')
        # Limit length
        if len(filename) > 200:
            filename = filename[:200]
        return filename or "webpage"

    def extract_title(self, soup):
        """Extract page title with fallbacks"""
        # Try different title sources in order of preference
        title_sources = [
            lambda: soup.find('meta', property='og:title'),
            lambda: soup.find('meta', name='twitter:title'),
            lambda: soup.find('h1'),
            lambda: soup.find('title')
        ]
        
        for source in title_sources:
            try:
                element = source()
                if element:
                    if element.name == 'meta':
                        title = element.get('content', '').strip()
                    else:
                        title = element.get_text().strip()
                    
                    if title and len(title) > 3:
                        return title
            except:
                continue
        
        return "Untitled"

    def clean_content(self, soup, url):
        """Remove unwanted elements and clean up the content"""
        # Remove script, style, nav, footer, ads, etc.
        unwanted_tags = [
            'script', 'style', 'nav', 'footer', 'header', 'aside',
            'iframe', 'noscript', 'form', 'button', 'input'
        ]
        
        for tag in unwanted_tags:
            for element in soup.find_all(tag):
                element.decompose()
        
        # Remove elements with common ad/navigation class names
        unwanted_classes = [
            'nav', 'navigation', 'menu', 'sidebar', 'footer', 'header',
            'ad', 'ads', 'advertisement', 'banner', 'popup', 'modal',
            'cookie', 'subscribe', 'newsletter', 'social', 'share',
            'comment', 'related', 'recommendation'
        ]
        
        for class_name in unwanted_classes:
            for element in soup.find_all(class_=lambda x: x and any(unwanted in str(x).lower() for unwanted in [class_name])):
                element.decompose()
        
        # Try to find main content area
        main_content_selectors = [
            'article', 'main', '.content', '#content', '.post', '.entry',
            '.article', '[role="main"]', '.main-content'
        ]
        
        main_content = None
        for selector in main_content_selectors:
            main_content = soup.select_one(selector)
            if main_content:
                break
        
        # If we found a main content area, use only that
        if main_content:
            # Create new soup with just the main content
            new_soup = BeautifulSoup('<div></div>', 'html.parser')
            new_soup.div.append(main_content)
            soup = new_soup
        
        # Convert relative URLs to absolute
        base_url = url.rsplit('/', 1)[0]
        for img in soup.find_all('img', src=True):
            img['src'] = urljoin(url, img['src'])
        
        for link in soup.find_all('a', href=True):
            link['href'] = urljoin(url, link['href'])
        
        return soup

    def fetch_and_convert(self, url, output_filename=None):
        """Fetch URL and convert to markdown"""
        print(f"🌐 Fetching: {url}")
        
        try:
            # Validate URL
            parsed = urlparse(url)
            if not parsed.scheme:
                url = 'https://' + url
                parsed = urlparse(url)
            
            # Fetch the page
            response = requests.get(url, headers=self.headers, timeout=30)
            response.raise_for_status()
            
            print(f"✅ Successfully fetched ({response.status_code})")
            
            # Parse HTML
            soup = BeautifulSoup(response.content, 'html.parser')
            
            # Extract title
            title = self.extract_title(soup)
            print(f"📰 Title: {title}")
            
            # Clean content
            cleaned_soup = self.clean_content(soup, url)
            
            # Convert to markdown
            markdown_content = self.h.handle(str(cleaned_soup))
            
            # Add metadata header
            metadata = f"""# {title}

**Source:** {url}  
**Fetched:** {time.strftime('%Y-%m-%d %H:%M:%S')}

---

"""
            
            final_content = metadata + markdown_content.strip()
            
            # Determine output filename
            if not output_filename:
                output_filename = self.clean_filename(title)
            
            if not output_filename.endswith('.md'):
                output_filename += '.md'
            
            # Save to file
            output_path = self.output_dir / output_filename
            
            # Handle file conflicts
            counter = 1
            original_path = output_path
            while output_path.exists():
                name_part = original_path.stem
                output_path = self.output_dir / f"{name_part}_{counter}.md"
                counter += 1
            
            with open(output_path, 'w', encoding='utf-8') as f:
                f.write(final_content)
            
            print(f"💾 Saved: {output_path}")
            print(f"📊 Content length: {len(final_content)} characters")
            
            return output_path
            
        except requests.RequestException as e:
            print(f"❌ Error fetching URL: {e}")
            return None
        except Exception as e:
            print(f"❌ Error processing content: {e}")
            return None

    def interactive_mode(self):
        """Run in interactive mode"""
        print("🔄 Web to Markdown Converter")
        print("=" * 40)
        
        while True:
            print("\n📝 Enter a URL to convert (or 'quit' to exit):")
            url = input("URL: ").strip()
            
            if url.lower() in ['quit', 'exit', 'q']:
                print("👋 Goodbye!")
                break
            
            if not url:
                print("❌ Please enter a valid URL")
                continue
            
            print("\n📁 Enter output filename (optional, press Enter for auto):")
            filename = input("Filename: ").strip()
            
            if not filename:
                filename = None
            
            print()  # Empty line for better readability
            result = self.fetch_and_convert(url, filename)
            
            if result:
                print(f"✨ Successfully converted and saved to: {result}")
                
                # Ask if user wants to open the file
                open_file = input("\n🔍 Open the markdown file? (y/n): ").strip().lower()
                if open_file in ['y', 'yes']:
                    try:
                        os.startfile(result)  # Windows
                    except AttributeError:
                        try:
                            os.system(f'open "{result}"')  # macOS
                        except:
                            os.system(f'xdg-open "{result}"')  # Linux
                    except Exception as e:
                        print(f"❌ Could not open file: {e}")
            
            print("\n" + "─" * 40)

def main():
    """Main function"""
    converter = WebToMarkdown()
    
    # Check if URL provided as command line argument
    if len(sys.argv) > 1:
        url = sys.argv[1]
        filename = sys.argv[2] if len(sys.argv) > 2 else None
        converter.fetch_and_convert(url, filename)
    else:
        # Run in interactive mode
        converter.interactive_mode()

if __name__ == "__main__":
    main()
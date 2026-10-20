HTML  to  Markdown


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTML to Markdown Converter Pro</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            font-weight: 700;
        }

        .header p {
            opacity: 0.9;
            font-size: 1.1rem;
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 0;
            min-height: 600px;
        }

        .input-section, .output-section {
            display: flex;
            flex-direction: column;
            background: white;
        }

        .input-section {
            border-right: 2px solid #f0f0f0;
        }

        .section-header {
            background: #f8fafc;
            padding: 20px;
            border-bottom: 1px solid #e2e8f0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .section-title {
            font-weight: 600;
            color: #334155;
            font-size: 1.1rem;
        }

        .controls {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .btn {
            padding: 8px 16px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 0.9rem;
            font-weight: 500;
            transition: all 0.2s ease;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }

        .btn-primary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: #e2e8f0;
            color: #64748b;
        }

        .btn-secondary:hover {
            background: #cbd5e1;
            transform: translateY(-1px);
        }

        .btn-success {
            background: #10b981;
            color: white;
        }

        .btn-success:hover {
            background: #059669;
            transform: translateY(-1px);
        }

        .textarea-container {
            flex: 1;
            display: flex;
            flex-direction: column;
        }

        .textarea {
            flex: 1;
            border: none;
            padding: 20px;
            font-family: 'SF Mono', Monaco, 'Cascadia Code', 'Roboto Mono', Consolas, 'Courier New', monospace;
            font-size: 14px;
            line-height: 1.6;
            resize: none;
            outline: none;
            background: #fefefe;
        }

        .textarea:focus {
            background: #fff;
        }

        .output-textarea {
            background: #f8fafc;
            color: #334155;
        }

        .stats {
            padding: 15px 20px;
            background: #f1f5f9;
            border-top: 1px solid #e2e8f0;
            font-size: 0.85rem;
            color: #64748b;
            display: flex;
            justify-content: space-between;
        }

        .feature-pills {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 15px;
        }

        .pill {
            background: rgba(255, 255, 255, 0.2);
            color: white;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 500;
        }

        .toast {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #10b981;
            color: white;
            padding: 16px 24px;
            border-radius: 12px;
            font-weight: 500;
            transform: translateX(400px);
            transition: transform 0.3s ease;
            z-index: 1000;
            box-shadow: 0 10px 25px rgba(16, 185, 129, 0.3);
        }

        .toast.show {
            transform: translateX(0);
        }

        .examples {
            margin-top: 20px;
        }

        .example-btn {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            color: white;
            padding: 6px 12px;
            border-radius: 6px;
            margin-right: 8px;
            margin-bottom: 8px;
            cursor: pointer;
            font-size: 0.8rem;
            transition: all 0.2s ease;
        }

        .example-btn:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-1px);
        }

        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .input-section {
                border-right: none;
                border-bottom: 2px solid #f0f0f0;
            }
            
            .header h1 {
                font-size: 2rem;
            }
            
            .controls {
                flex-wrap: wrap;
            }
        }

        .loading {
            opacity: 0.6;
            pointer-events: none;
        }

        .loading .btn-primary::after {
            content: '';
            width: 16px;
            height: 16px;
            border: 2px solid transparent;
            border-top: 2px solid white;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-left: 8px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>HTML to Markdown Converter Pro</h1>
            <p>Convert HTML to clean, readable Markdown with advanced formatting support</p>
            <div class="feature-pills">
                <span class="pill">Tables</span>
                <span class="pill">Code Blocks</span>
                <span class="pill">Links & Images</span>
                <span class="pill">Lists</span>
                <span class="pill">Headings</span>
                <span class="pill">Text Formatting</span>
            </div>
            <div class="examples">
                <button class="example-btn" onclick="loadExample('basic')">Basic HTML</button>
                <button class="example-btn" onclick="loadExample('table')">Table</button>
                <button class="example-btn" onclick="loadExample('complex')">Complex Document</button>
            </div>
        </div>
        
        <div class="main-content">
            <div class="input-section">
                <div class="section-header">
                    <span class="section-title">HTML Input</span>
                    <div class="controls">
                        <button class="btn btn-secondary" onclick="clearInput()">Clear</button>
                        <button class="btn btn-secondary" onclick="formatHTML()">Format HTML</button>
                    </div>
                </div>
                <div class="textarea-container">
                    <textarea 
                        id="html-input" 
                        class="textarea" 
                        placeholder="Paste your HTML code here or try one of the examples above..."
                        oninput="convertHTML()"
                    ></textarea>
                    <div class="stats">
                        <span id="input-stats">0 characters</span>
                        <span id="input-lines">0 lines</span>
                    </div>
                </div>
            </div>
            
            <div class="output-section">
                <div class="section-header">
                    <span class="section-title">Markdown Output</span>
                    <div class="controls">
                        <button class="btn btn-success" onclick="copyToClipboard()">📋 Copy</button>
                        <button class="btn btn-secondary" onclick="downloadMarkdown()">💾 Download</button>
                    </div>
                </div>
                <div class="textarea-container">
                    <textarea 
                        id="markdown-output" 
                        class="textarea output-textarea" 
                        readonly
                        placeholder="Converted Markdown will appear here..."
                    ></textarea>
                    <div class="stats">
                        <span id="output-stats">0 characters</span>
                        <span id="output-lines">0 lines</span>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div id="toast" class="toast"></div>

    <script>
        // Advanced HTML to Markdown converter
        class HTMLToMarkdownConverter {
            constructor() {
                this.rules = [
                    // Headers (h1-h6)
                    { pattern: /<h1[^>]*>([\s\S]*?)<\/h1>/gi, replacement: '# $1\n\n' },
                    { pattern: /<h2[^>]*>([\s\S]*?)<\/h2>/gi, replacement: '## $1\n\n' },
                    { pattern: /<h3[^>]*>([\s\S]*?)<\/h3>/gi, replacement: '### $1\n\n' },
                    { pattern: /<h4[^>]*>([\s\S]*?)<\/h4>/gi, replacement: '#### $1\n\n' },
                    { pattern: /<h5[^>]*>([\s\S]*?)<\/h5>/gi, replacement: '##### $1\n\n' },
                    { pattern: /<h6[^>]*>([\s\S]*?)<\/h6>/gi, replacement: '###### $1\n\n' },
                    
                    // Text formatting
                    { pattern: /<strong[^>]*>([\s\S]*?)<\/strong>/gi, replacement: '**$1**' },
                    { pattern: /<b[^>]*>([\s\S]*?)<\/b>/gi, replacement: '**$1**' },
                    { pattern: /<em[^>]*>([\s\S]*?)<\/em>/gi, replacement: '*$1*' },
                    { pattern: /<i[^>]*>([\s\S]*?)<\/i>/gi, replacement: '*$1*' },
                    { pattern: /<del[^>]*>([\s\S]*?)<\/del>/gi, replacement: '~~$1~~' },
                    { pattern: /<s[^>]*>([\s\S]*?)<\/s>/gi, replacement: '~~$1~~' },
                    { pattern: /<u[^>]*>([\s\S]*?)<\/u>/gi, replacement: '$1' },
                    
                    // Code
                    { pattern: /<code[^>]*>([\s\S]*?)<\/code>/gi, replacement: '`$1`' },
                    
                    // Links and Images
                    { pattern: /<a[^>]*href\s*=\s*["']([^"']*)["'][^>]*>([\s\S]*?)<\/a>/gi, replacement: '[$2]($1)' },
                    { pattern: /<img[^>]*src\s*=\s*["']([^"']*)["'][^>]*alt\s*=\s*["']([^"']*)["'][^>]*\/?>/gi, replacement: '![$2]($1)' },
                    { pattern: /<img[^>]*alt\s*=\s*["']([^"']*)["'][^>]*src\s*=\s*["']([^"']*)["'][^>]*\/?>/gi, replacement: '![$1]($2)' },
                    { pattern: /<img[^>]*src\s*=\s*["']([^"']*)["'][^>]*\/?>/gi, replacement: '![]($1)' },
                    
                    // Paragraphs and line breaks
                    { pattern: /<p[^>]*>/gi, replacement: '' },
                    { pattern: /<\/p>/gi, replacement: '\n\n' },
                    { pattern: /<br\s*\/?>/gi, replacement: '\n' },
                    
                    // Horizontal rule
                    { pattern: /<hr[^>]*\/?>/gi, replacement: '\n---\n\n' },
                    
                    // Blockquotes
                    { pattern: /<blockquote[^>]*>([\s\S]*?)<\/blockquote>/gi, replacement: (match, content) => {
                        return content.trim().split('\n').map(line => '> ' + line.trim()).join('\n') + '\n\n';
                    }},
                ];
            }

            convert(html) {
                let markdown = html;
                
                // Handle pre and code blocks first
                markdown = this.handleCodeBlocks(markdown);
                
                // Handle tables
                markdown = this.handleTables(markdown);
                
                // Handle lists
                markdown = this.handleLists(markdown);
                
                // Apply basic rules
                for (const rule of this.rules) {
                    if (typeof rule.replacement === 'function') {
                        markdown = markdown.replace(rule.pattern, rule.replacement);
                    } else {
                        markdown = markdown.replace(rule.pattern, rule.replacement);
                    }
                }
                
                // Clean up HTML tags and entities
                markdown = this.cleanupHTML(markdown);
                
                // Clean up extra whitespace
                markdown = this.cleanupWhitespace(markdown);
                
                return markdown;
            }

            handleCodeBlocks(html) {
                // Handle <pre><code> blocks
                html = html.replace(/<pre[^>]*><code[^>]*>([\s\S]*?)<\/code><\/pre>/gi, (match, content) => {
                    const cleanContent = this.decodeEntities(content.trim());
                    return '\n```\n' + cleanContent + '\n```\n\n';
                });
                
                // Handle standalone <pre> blocks
                html = html.replace(/<pre[^>]*>([\s\S]*?)<\/pre>/gi, (match, content) => {
                    const cleanContent = this.decodeEntities(content.trim());
                    return '\n```\n' + cleanContent + '\n```\n\n';
                });
                
                return html;
            }

            handleTables(html) {
                return html.replace(/<table[^>]*>([\s\S]*?)<\/table>/gi, (match, tableContent) => {
                    const rows = [];
                    let headerProcessed = false;
                    
                    // Extract table rows
                    const rowMatches = tableContent.match(/<tr[^>]*>([\s\S]*?)<\/tr>/gi);
                    if (!rowMatches) return match;
                    
                    for (const rowMatch of rowMatches) {
                        const cells = [];
                        const cellMatches = rowMatch.match(/<t[hd][^>]*>([\s\S]*?)<\/t[hd]>/gi);
                        
                        if (cellMatches) {
                            for (const cellMatch of cellMatches) {
                                const cellContent = cellMatch.replace(/<t[hd][^>]*>([\s\S]*?)<\/t[hd]>/gi, '$1').trim();
                                cells.push(this.stripTags(cellContent));
                            }
                            
                            rows.push('| ' + cells.join(' | ') + ' |');
                            
                            // Add separator after header row
                            if (!headerProcessed && rowMatch.includes('<th')) {
                                const separator = '| ' + cells.map(() => '---').join(' | ') + ' |';
                                rows.push(separator);
                                headerProcessed = true;
                            }
                        }
                    }
                    
                    return '\n' + rows.join('\n') + '\n\n';
                });
            }

            handleLists(html) {
                // Handle unordered lists
                html = html.replace(/<ul[^>]*>([\s\S]*?)<\/ul>/gi, (match, listContent) => {
                    const items = listContent.match(/<li[^>]*>([\s\S]*?)<\/li>/gi);
                    if (!items) return match;
                    
                    const listItems = items.map(item => {
                        const content = item.replace(/<li[^>]*>([\s\S]*?)<\/li>/gi, '$1').trim();
                        return '- ' + this.stripTags(content);
                    });
                    
                    return '\n' + listItems.join('\n') + '\n\n';
                });
                
                // Handle ordered lists
                html = html.replace(/<ol[^>]*>([\s\S]*?)<\/ol>/gi, (match, listContent) => {
                    const items = listContent.match(/<li[^>]*>([\s\S]*?)<\/li>/gi);
                    if (!items) return match;
                    
                    const listItems = items.map((item, index) => {
                        const content = item.replace(/<li[^>]*>([\s\S]*?)<\/li>/gi, '$1').trim();
                        return `${index + 1}. ${this.stripTags(content)}`;
                    });
                    
                    return '\n' + listItems.join('\n') + '\n\n';
                });
                
                return html;
            }

            stripTags(html) {
                return html.replace(/<[^>]*>/g, '');
            }

            cleanupHTML(html) {
                // Remove remaining HTML tags
                html = html.replace(/<[^>]*>/g, '');
                
                // Decode HTML entities
                html = this.decodeEntities(html);
                
                return html;
            }

            decodeEntities(text) {
                const entities = {
                    '&amp;': '&',
                    '&lt;': '<',
                    '&gt;': '>',
                    '&quot;': '"',
                    '&#39;': "'",
                    '&nbsp;': ' ',
                    '&mdash;': '—',
                    '&ndash;': '–',
                    '&hellip;': '…'
                };
                
                for (const [entity, char] of Object.entries(entities)) {
                    text = text.replace(new RegExp(entity, 'g'), char);
                }
                
                return text;
            }

            cleanupWhitespace(markdown) {
                // Remove excessive blank lines
                markdown = markdown.replace(/\n{3,}/g, '\n\n');
                
                // Trim whitespace from lines
                markdown = markdown.split('\n').map(line => line.trimEnd()).join('\n');
                
                // Remove leading/trailing whitespace
                markdown = markdown.trim();
                
                return markdown;
            }
        }

        // Initialize converter
        const converter = new HTMLToMarkdownConverter();

        // DOM elements
        const htmlInput = document.getElementById('html-input');
        const markdownOutput = document.getElementById('markdown-output');
        const inputStats = document.getElementById('input-stats');
        const inputLines = document.getElementById('input-lines');
        const outputStats = document.getElementById('output-stats');
        const outputLines = document.getElementById('output-lines');
        const toast = document.getElementById('toast');

        // Convert HTML to Markdown
        function convertHTML() {
            const html = htmlInput.value;
            updateStats();
            
            if (!html.trim()) {
                markdownOutput.value = '';
                return;
            }
            
            try {
                const markdown = converter.convert(html);
                markdownOutput.value = markdown;
            } catch (error) {
                markdownOutput.value = 'Error converting HTML: ' + error.message;
            }
        }

        // Update statistics
        function updateStats() {
            const htmlText = htmlInput.value;
            const markdownText = markdownOutput.value;
            
            inputStats.textContent = `${htmlText.length} characters`;
            inputLines.textContent = `${htmlText.split('\n').length} lines`;
            
            outputStats.textContent = `${markdownText.length} characters`;
            outputLines.textContent = `${markdownText.split('\n').length} lines`;
        }

        // Clear input
        function clearInput() {
            htmlInput.value = '';
            markdownOutput.value = '';
            updateStats();
            htmlInput.focus();
        }

        // Format HTML (basic indentation)
        function formatHTML() {
            const html = htmlInput.value;
            if (!html.trim()) return;
            
            try {
                const formatted = html
                    .replace(/></g, '>\n<')
                    .replace(/^\s+|\s+$/gm, '')
                    .split('\n')
                    .map(line => line.trim())
                    .filter(line => line)
                    .join('\n');
                
                htmlInput.value = formatted;
                convertHTML();
            } catch (error) {
                showToast('Error formatting HTML');
            }
        }

        // Copy to clipboard
        async function copyToClipboard() {
            const markdown = markdownOutput.value;
            if (!markdown.trim()) {
                showToast('Nothing to copy');
                return;
            }
            
            try {
                await navigator.clipboard.writeText(markdown);
                showToast('Copied to clipboard!');
            } catch (error) {
                // Fallback for older browsers
                markdownOutput.select();
                document.execCommand('copy');
                showToast('Copied to clipboard!');
            }
        }

        // Download markdown file
        function downloadMarkdown() {
            const markdown = markdownOutput.value;
            if (!markdown.trim()) {
                showToast('Nothing to download');
                return;
            }
            
            const blob = new Blob([markdown], { type: 'text/markdown' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'converted.md';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            showToast('Markdown file downloaded!');
        }

        // Show toast notification
        function showToast(message) {
            toast.textContent = message;
            toast.classList.add('show');
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        // Load example content
        function loadExample(type) {
            const examples = {
                basic: `<h1>Welcome to My Blog</h1>
<p>This is a <strong>sample blog post</strong> with various <em>formatting elements</em>.</p>
<p>Here's a <a href="https://example.com">link to my website</a> and an image:</p>
<img src="https://via.placeholder.com/300x200" alt="Sample Image" />
<h2>Features</h2>
<ul>
<li>Easy to use</li>
<li>Fast conversion</li>
<li>Clean output</li>
</ul>`,

                table: `<h2>Product Comparison</h2>
<table>
<thead>
<tr>
<th>Product</th>
<th>Price</th>
<th>Rating</th>
<th>Available</th>
</tr>
</thead>
<tbody>
<tr>
<td>Widget A</td>
<td>$19.99</td>
<td>4.5/5</td>
<td>Yes</td>
</tr>
<tr>
<td>Widget B</td>
<td>$24.99</td>
<td>4.2/5</td>
<td>No</td>
</tr>
<tr>
<td>Widget C</td>
<td>$29.99</td>
<td>4.8/5</td>
<td>Yes</td>
</tr>
</tbody>
</table>`,

                complex: `<h1>Technical Documentation</h1>
<p>This document demonstrates <strong>advanced HTML features</strong> and their conversion to Markdown.</p>

<h2>Code Examples</h2>
<p>Here's how to create a simple function:</p>
<pre><code>function greet(name) {
    return "Hello, " + name + "!";
}

console.log(greet("World"));</code></pre>

<h2>Important Information</h2>
<blockquote>
<p>This is a blockquote with <em>emphasis</em> and a <a href="#">link</a>.</p>
<p>It can span multiple paragraphs.</p>
</blockquote>

<h3>Task List</h3>
<ol>
<li>Review the documentation</li>
<li>Test the conversion</li>
<li>Deploy to production</li>
</ol>

<hr>

<p><del>This text is crossed out</del> while this text is <u>underlined</u>.</p>`
            };
            
            htmlInput.value = examples[type] || '';
            convertHTML();
            htmlInput.focus();
        }

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            updateStats();
            htmlInput.focus();
            
            // Auto-resize textareas
            function autoResize(textarea) {
                textarea.style.height = 'auto';
                textarea.style.height = textarea.scrollHeight + 'px';
            }
            
            htmlInput.addEventListener('input', function() {
                convertHTML();
            });
            
            markdownOutput.addEventListener('input', updateStats);
        });

        // Keyboard shortcuts
        document.addEventListener('keydown', function(e) {
            // Ctrl+Enter to convert
            if (e.ctrlKey && e.key === 'Enter') {
                e.preventDefault();
                convertHTML();
            }
            
            // Ctrl+K to clear
            if (e.ctrlKey && e.key === 'k') {
                e.preventDefault();
                clearInput();
            }
            
            // Ctrl+S to download
            if (e.ctrlKey && e.key === 's') {
                e.preventDefault();
                downloadMarkdown();
            }
        });
    </script>
</body>
</html>
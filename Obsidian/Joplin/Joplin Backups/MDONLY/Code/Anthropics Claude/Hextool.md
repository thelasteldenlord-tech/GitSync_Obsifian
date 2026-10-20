Hextool
```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Photo Color Hex Extractor</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #ff6b6b, #ffa726);
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
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .upload-section {
            padding: 40px;
            text-align: center;
        }

        .upload-area {
            border: 3px dashed #ddd;
            border-radius: 15px;
            padding: 60px 20px;
            margin-bottom: 30px;
            transition: all 0.3s ease;
            cursor: pointer;
            background: #fafafa;
        }

        .upload-area:hover, .upload-area.dragover {
            border-color: #ff6b6b;
            background: #fff5f5;
            transform: translateY(-2px);
        }

        .upload-icon {
            font-size: 4rem;
            color: #ddd;
            margin-bottom: 20px;
        }

        .upload-area:hover .upload-icon {
            color: #ff6b6b;
        }

        .upload-text {
            font-size: 1.2rem;
            color: #666;
            margin-bottom: 15px;
        }

        .file-input {
            display: none;
        }

        .btn {
            background: linear-gradient(135deg, #ff6b6b, #ffa726);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(255, 107, 107, 0.4);
        }

        .preview-section {
            padding: 0 40px 20px;
            display: none;
        }

        .image-preview {
            max-width: 100%;
            max-height: 400px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            margin-bottom: 30px;
        }

        .colors-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .color-item {
            background: white;
            border-radius: 10px;
            padding: 15px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }

        .color-item:hover {
            transform: translateY(-5px);
        }

        .color-swatch {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            margin: 0 auto 10px;
            border: 3px solid white;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
        }

        .color-hex {
            font-family: 'Courier New', monospace;
            font-weight: bold;
            font-size: 0.9rem;
            color: #333;
            cursor: pointer;
            padding: 5px;
            border-radius: 5px;
            transition: background 0.3s ease;
        }

        .color-hex:hover {
            background: #f0f0f0;
        }

        .loading {
            display: none;
            text-align: center;
            padding: 20px;
        }

        .spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #ff6b6b;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 0 auto 15px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .results-header {
            text-align: center;
            margin-bottom: 20px;
            font-size: 1.3rem;
            color: #333;
            font-weight: 600;
        }

        .export-section {
            text-align: center;
            margin: 30px 0;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 15px;
        }

        .export-buttons {
            display: flex;
            gap: 15px;
            justify-content: center;
            flex-wrap: wrap;
            margin-top: 15px;
        }

        .export-btn {
            background: linear-gradient(135deg, #28a745, #20c997);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 20px;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 3px 10px rgba(40, 167, 69, 0.3);
        }

        .export-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(40, 167, 69, 0.4);
        }

        .export-btn.css {
            background: linear-gradient(135deg, #6f42c1, #e83e8c);
        }

        .export-btn.css:hover {
            box-shadow: 0 6px 20px rgba(111, 66, 193, 0.4);
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🎨 Color Extractor</h1>
            <p>Upload a photo and discover its dominant colors with hex values</p>
        </div>
        
        <div class="upload-section">
            <div class="upload-area" onclick="document.getElementById('fileInput').click()" ondrop="handleDrop(event)" ondragover="handleDragOver(event)" ondragleave="handleDragLeave(event)">
                <div class="upload-icon">📸</div>
                <div class="upload-text">Drop your image here or click to browse</div>
                <button class="btn" type="button">Choose Photo</button>
            </div>
            <input type="file" id="fileInput" class="file-input" accept="image/*" onchange="handleFileSelect(event)">
        </div>

        <div class="loading">
            <div class="spinner"></div>
            <p>Analyzing colors...</p>
        </div>

        <div class="preview-section">
            <img id="imagePreview" class="image-preview" alt="Uploaded image">
            <div class="results-header">Dominant Colors</div>
            <div id="colorsGrid" class="colors-grid"></div>
            
            <div class="export-section">
                <h3>Export Colors</h3>
                <p>Download your color palette for easy use in CSS themes</p>
                <div class="export-buttons">
                    <button class="export-btn" onclick="exportAsCSV()">📊 Export as CSV</button>
                    <button class="export-btn" onclick="exportAsText()">📄 Export as Text</button>
                    <button class="export-btn css" onclick="exportAsCSS()">🎨 Export as CSS Variables</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        function handleDragOver(e) {
            e.preventDefault();
            e.currentTarget.classList.add('dragover');
        }

        function handleDragLeave(e) {
            e.currentTarget.classList.remove('dragover');
        }

        function handleDrop(e) {
            e.preventDefault();
            e.currentTarget.classList.remove('dragover');
            const files = e.dataTransfer.files;
            if (files.length > 0) {
                processFile(files[0]);
            }
        }

        function handleFileSelect(e) {
            const file = e.target.files[0];
            if (file) {
                processFile(file);
            }
        }

        function processFile(file) {
            if (!file.type.startsWith('image/')) {
                alert('Please select an image file.');
                return;
            }

            const reader = new FileReader();
            reader.onload = function(e) {
                showLoading();
                const img = new Image();
                img.onload = function() {
                    extractColors(img);
                };
                img.src = e.target.result;
                document.getElementById('imagePreview').src = e.target.result;
            };
            reader.readAsDataURL(file);
        }

        function showLoading() {
            document.querySelector('.loading').style.display = 'block';
            document.querySelector('.preview-section').style.display = 'none';
        }

        function extractColors(img) {
            const canvas = document.createElement('canvas');
            const ctx = canvas.getContext('2d');
            
            // Resize for performance
            const maxSize = 300;
            const ratio = Math.min(maxSize / img.width, maxSize / img.height);
            canvas.width = img.width * ratio;
            canvas.height = img.height * ratio;
            
            ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
            
            const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
            const data = imageData.data;
            
            const colorMap = new Map();
            
            // Sample every 4th pixel for performance
            for (let i = 0; i < data.length; i += 16) {
                const r = data[i];
                const g = data[i + 1];
                const b = data[i + 2];
                const alpha = data[i + 3];
                
                if (alpha < 128) continue; // Skip transparent pixels
                
                // Group similar colors
                const key = `${Math.floor(r/10)*10},${Math.floor(g/10)*10},${Math.floor(b/10)*10}`;
                colorMap.set(key, (colorMap.get(key) || 0) + 1);
            }
            
            // Get most frequent colors
            const sortedColors = Array.from(colorMap.entries())
                .sort((a, b) => b[1] - a[1])
                .slice(0, 12)
                .map(([color]) => {
                    const [r, g, b] = color.split(',').map(Number);
                    return { r, g, b };
                });
            
            displayColors(sortedColors);
        }

        function displayColors(colors) {
            const grid = document.getElementById('colorsGrid');
            grid.innerHTML = '';
            
            // Store colors globally for export
            extractedColors = colors;
            
            colors.forEach(color => {
                const hex = rgbToHex(color.r, color.g, color.b);
                const colorItem = document.createElement('div');
                colorItem.className = 'color-item';
                colorItem.innerHTML = `
                    <div class="color-swatch" style="background-color: ${hex}"></div>
                    <div class="color-hex" onclick="copyToClipboard('${hex}')" title="Click to copy">${hex}</div>
                `;
                grid.appendChild(colorItem);
            });
            
            document.querySelector('.loading').style.display = 'none';
            document.querySelector('.preview-section').style.display = 'block';
        }

        function rgbToHex(r, g, b) {
            return "#" + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1).toUpperCase();
        }

        function copyToClipboard(text) {
            navigator.clipboard.writeText(text).then(() => {
                // Visual feedback
                const temp = document.createElement('div');
                temp.style.cssText = 'position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);background:#333;color:white;padding:10px 20px;border-radius:5px;z-index:1000;';
                temp.textContent = `Copied ${text}!`;
                document.body.appendChild(temp);
                setTimeout(() => document.body.removeChild(temp), 1500);
            });
        }

        // Store extracted colors globally for export
        let extractedColors = [];

        function exportAsCSV() {
            if (extractedColors.length === 0) {
                alert('No colors to export. Please upload an image first.');
                return;
            }
            
            let csvContent = "Color Name,Hex Code,RGB Values\n";
            extractedColors.forEach((color, index) => {
                const hex = rgbToHex(color.r, color.g, color.b);
                csvContent += `Color ${index + 1},${hex},"rgb(${color.r}, ${color.g}, ${color.b})"\n`;
            });
            
            downloadFile(csvContent, 'photo-colors.csv', 'text/csv');
        }

        function exportAsText() {
            if (extractedColors.length === 0) {
                alert('No colors to export. Please upload an image first.');
                return;
            }
            
            let textContent = "Photo Color Palette\n";
            textContent += "==================\n\n";
            extractedColors.forEach((color, index) => {
                const hex = rgbToHex(color.r, color.g, color.b);
                textContent += `Color ${index + 1}: ${hex} (RGB: ${color.r}, ${color.g}, ${color.b})\n`;
            });
            
            downloadFile(textContent, 'photo-colors.txt', 'text/plain');
        }

        function exportAsCSS() {
            if (extractedColors.length === 0) {
                alert('No colors to export. Please upload an image first.');
                return;
            }
            
            let cssContent = "/* Photo Color Palette - CSS Variables */\n";
            cssContent += ":root {\n";
            extractedColors.forEach((color, index) => {
                const hex = rgbToHex(color.r, color.g, color.b);
                cssContent += `  --color-${index + 1}: ${hex};\n`;
                cssContent += `  --color-${index + 1}-rgb: ${color.r}, ${color.g}, ${color.b};\n`;
            });
            cssContent += "}\n\n";
            cssContent += "/* Usage Examples */\n";
            cssContent += "/* .primary-bg { background-color: var(--color-1); } */\n";
            cssContent += "/* .accent-text { color: var(--color-2); } */\n";
            cssContent += "/* .transparent-bg { background-color: rgba(var(--color-3-rgb), 0.5); } */\n";
            
            downloadFile(cssContent, 'photo-colors.css', 'text/css');
        }

        function downloadFile(content, filename, mimeType) {
            try {
                const blob = new Blob([content], { type: mimeType });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = filename;
                a.style.display = 'none';
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                
                // Show success message
                showMessage(`${filename} downloaded successfully!`, '#28a745');
            } catch (error) {
                console.error('Download failed:', error);
                showMessage('Download failed. Please try again.', '#dc3545');
            }
        }

        function showMessage(text, color) {
            const temp = document.createElement('div');
            temp.style.cssText = `position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);background:${color};color:white;padding:15px 25px;border-radius:8px;z-index:1000;font-weight:bold;box-shadow:0 4px 20px rgba(0,0,0,0.3);`;
            temp.textContent = text;
            document.body.appendChild(temp);
            setTimeout(() => {
                if (document.body.contains(temp)) {
                    document.body.removeChild(temp);
                }
            }, 2000);
        }
    </script>
</body>
</html>
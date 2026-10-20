# Handy to to

```html


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Brush Cutting Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Arial Black', Arial, sans-serif;
            background: linear-gradient(135deg, #2d5016, #4a7c20);
            color: white;
            padding: 10px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 400px;
            margin: 0 auto;
            background: rgba(0,0,0,0.3);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }
        
        h1 {
            text-align: center;
            color: #90EE90;
            margin-bottom: 20px;
            font-size: 1.8em;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
        }
        
        .clicker-section {
            text-align: center;
            margin-bottom: 30px;
        }
        
        .big-button {
            width: 200px;
            height: 200px;
            border-radius: 50%;
            background: linear-gradient(145deg, #ff6b35, #f7931e);
            border: 8px solid #fff;
            color: white;
            font-size: 2.5em;
            font-weight: bold;
            cursor: pointer;
            margin: 20px auto;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            box-shadow: 0 8px 25px rgba(0,0,0,0.4);
            transition: all 0.1s ease;
            user-select: none;
        }
        
        .big-button:active {
            transform: scale(0.95);
            box-shadow: 0 4px 15px rgba(0,0,0,0.6);
        }
        
        .counter {
            font-size: 3em;
            font-weight: bold;
            color: #90EE90;
            margin: 15px 0;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
        }
        
        .stats {
            background: rgba(255,255,255,0.1);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
        }
        
        .stat-row {
            display: flex;
            justify-content: space-between;
            margin: 10px 0;
            font-size: 1.2em;
        }
        
        .stat-label {
            color: #FFD700;
            font-weight: bold;
        }
        
        .stat-value {
            color: white;
            font-weight: bold;
        }
        
        .pricing {
            background: linear-gradient(135deg, #ff6b35, #f7931e);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            margin-bottom: 20px;
        }
        
        .price-title {
            font-size: 1.3em;
            margin-bottom: 10px;
            color: white;
        }
        
        .price-amount {
            font-size: 2.5em;
            font-weight: bold;
            color: white;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }
        
        .controls {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }
        
        .control-btn {
            flex: 1;
            padding: 15px;
            border: none;
            border-radius: 10px;
            font-size: 1.1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        
        .reset-btn {
            background: #dc3545;
            color: white;
        }
        
        .reset-btn:hover {
            background: #c82333;
        }
        
        .minus-btn {
            background: #ffc107;
            color: black;
        }
        
        .minus-btn:hover {
            background: #e0a800;
        }
        
        .footer {
            text-align: center;
            margin-top: 20px;
            font-size: 0.9em;
            color: #90EE90;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🌿 Brush Cutting Calculator 🌿</h1>
        
        <div class="clicker-section">
            <div class="big-button" onclick="addSection()">
                CLICK<br>+25 FT
            </div>
            <div class="counter" id="sectionCount">0</div>
            <div style="color: #FFD700; font-size: 1.2em; font-weight: bold;">Sections Counted</div>
        </div>
        
        <div class="stats">
            <div class="stat-row">
                <span class="stat-label">Length:</span>
                <span class="stat-value" id="totalLength">0 ft</span>
            </div>
            <div class="stat-row">
                <span class="stat-label">Width:</span>
                <span class="stat-value">4 ft</span>
            </div>
            <div class="stat-row">
                <span class="stat-label">Height:</span>
                <span class="stat-value">6 ft</span>
            </div>
            <div class="stat-row">
                <span class="stat-label">Area:</span>
                <span class="stat-value" id="totalArea">0 sq ft</span>
            </div>
        </div>
        
        <div class="pricing">
            <div class="price-title">Estimated Quote</div>
            <div class="price-amount" id="priceEstimate">$0</div>
            <div style="font-size: 0.9em; margin-top: 10px; opacity: 0.9;">
                @ $2.50 per sq ft for thick brush clearing
            </div>
        </div>
        
        <div class="controls">
            <button class="control-btn minus-btn" onclick="removeSection()">-1 Section</button>
            <button class="control-btn reset-btn" onclick="resetCounter()">Reset All</button>
        </div>
        
        <div class="footer">
            Tap the big orange button for each 25ft section!<br>
            Perfect for fence line brush clearing 🚜
        </div>
    </div>

    <script>
        let sectionCount = 0;
        const sectionLength = 25; // feet
        const brushWidth = 4; // feet
        const pricePerSqFt = 2.50; // dollars per square foot
        
        function addSection() {
            sectionCount++;
            updateDisplay();
            
            // Add some visual feedback
            const button = document.querySelector('.big-button');
            button.style.background = 'linear-gradient(145deg, #ff8c00, #ffa500)';
            setTimeout(() => {
                button.style.background = 'linear-gradient(145deg, #ff6b35, #f7931e)';
            }, 100);
        }
        
        function removeSection() {
            if (sectionCount > 0) {
                sectionCount--;
                updateDisplay();
            }
        }
        
        function resetCounter() {
            sectionCount = 0;
            updateDisplay();
        }
        
        function updateDisplay() {
            const totalLength = sectionCount * sectionLength;
            const totalArea = totalLength * brushWidth;
            const priceEstimate = totalArea * pricePerSqFt;
            
            document.getElementById('sectionCount').textContent = sectionCount;
            document.getElementById('totalLength').textContent = totalLength + ' ft';
            document.getElementById('totalArea').textContent = totalArea.toLocaleString() + ' sq ft';
            document.getElementById('priceEstimate').textContent = '$' + priceEstimate.toLocaleString();
        }
        
        // Initialize display
        updateDisplay();
    </script>
</body>
</html>
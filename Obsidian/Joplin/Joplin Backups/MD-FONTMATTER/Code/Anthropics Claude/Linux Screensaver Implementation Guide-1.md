---
title: Linux Screensaver Implementation Guide
updated: 2025-09-02 07:29:54Z
created: 2025-09-02 07:29:51Z
---

# Linux Screensaver Implementation Guide

## Method 1: XScreenSaver + HTML (Easiest)

### Step 1: Install Dependencies
```bash
sudo pacman -S xscreensaver chromium
```

### Step 2: Create Screensaver Directory
```bash
mkdir -p ~/.config/xscreensaver/hacks
cd ~/.config/xscreensaver/hacks
```

### Step 3: Create HTML File
```bash
# Create geometric-screensaver.html
cat > geometric-screensaver.html << 'EOF'
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Geometric Screensaver</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background: #2B2420;
            overflow: hidden;
            font-family: Arial, sans-serif;
        }
        canvas {
            display: block;
        }
        .controls {
            position: fixed;
            top: 20px;
            right: 20px;
            color: #F4E8D0;
            background: rgba(43, 36, 32, 0.8);
            padding: 15px;
            border-radius: 8px;
            z-index: 1000;
        }
        .control-group {
            margin-bottom: 10px;
        }
        input[type="range"] {
            width: 150px;
        }
    </style>
</head>
<body>
    <div class="controls">
        <div class="control-group">
            <label>Speed: <span id="speedValue">1.0</span></label>
            <input type="range" id="speed" min="0.1" max="3.0" step="0.1" value="1.0">
        </div>
        <div class="control-group">
            <label>Polygons: <span id="polygonValue">6</span></label>
            <input type="range" id="polygonCount" min="3" max="15" step="1" value="6">
        </div>
        <div class="control-group">
            <label>Size: <span id="sizeValue">1.0</span></label>
            <input type="range" id="size" min="0.5" max="2.0" step="0.1" value="1.0">
        </div>
        <div class="control-group">
            <label>Layers: <span id="layerValue">3</span></label>
            <input type="range" id="layers" min="1" max="5" step="1" value="3">
        </div>
    </div>
    <canvas id="canvas"></canvas>

    <script>
        // Your converted JavaScript code goes here
        // (Convert the React useEffect content to vanilla JS)
        
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        
        // Make canvas fullscreen
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();
        
        // Global parameters (controllable)
        let params = {
            speed: 1.0,
            polygonCount: 6,
            size: 1.0,
            layers: 3
        };
        
        // Control handlers
        document.getElementById('speed').addEventListener('input', (e) => {
            params.speed = parseFloat(e.target.value);
            document.getElementById('speedValue').textContent = params.speed;
        });
        
        document.getElementById('polygonCount').addEventListener('input', (e) => {
            params.polygonCount = parseInt(e.target.value);
            document.getElementById('polygonValue').textContent = params.polygonCount;
        });
        
        document.getElementById('size').addEventListener('input', (e) => {
            params.size = parseFloat(e.target.value);
            document.getElementById('sizeValue').textContent = params.size;
        });
        
        document.getElementById('layers').addEventListener('input', (e) => {
            params.layers = parseInt(e.target.value);
            document.getElementById('layerValue').textContent = params.layers;
        });
        
        // Hide controls after 5 seconds of no mouse movement
        let controlsVisible = true;
        let hideTimeout;
        
        document.addEventListener('mousemove', () => {
            if (!controlsVisible) {
                document.querySelector('.controls').style.display = 'block';
                controlsVisible = true;
            }
            clearTimeout(hideTimeout);
            hideTimeout = setTimeout(() => {
                document.querySelector('.controls').style.display = 'none';
                controlsVisible = false;
            }, 5000);
        });
        
        // Animation code (adapted from your React component)
        let time = 0;
        const colors = {
            bg: '#2B2420',
            cream: '#F4E8D0',
            coffee: '#8B4513',
            darkCoffee: '#4A2C17',
            lightCream: '#FFF8E7',
            accent: '#D4A574',
            darkAccent: '#A0824A'
        };
        
        function drawPolygon(cx, cy, radius, sides, rotation, phase, layer) {
            ctx.save();
            ctx.translate(cx, cy);
            ctx.rotate(rotation);

            const gradient = ctx.createRadialGradient(0, 0, 0, 0, 0, radius);
            
            if (layer === 0) {
                gradient.addColorStop(0, colors.lightCream);
                gradient.addColorStop(0.6, colors.cream);
                gradient.addColorStop(1, colors.coffee);
            } else if (layer === 1) {
                gradient.addColorStop(0, colors.accent);
                gradient.addColorStop(0.7, colors.coffee);
                gradient.addColorStop(1, colors.darkCoffee);
            } else {
                gradient.addColorStop(0, colors.cream);
                gradient.addColorStop(0.5, colors.darkAccent);
                gradient.addColorStop(1, colors.darkCoffee);
            }

            ctx.beginPath();
            for (let i = 0; i <= sides; i++) {
                const angle = (i / sides) * Math.PI * 2;
                const r = radius * (1 + Math.sin(phase + i * 0.5) * 0.1);
                const x = Math.cos(angle) * r;
                const y = Math.sin(angle) * r;
                if (i === 0) {
                    ctx.moveTo(x, y);
                } else {
                    ctx.lineTo(x, y);
                }
            }

            ctx.fillStyle = gradient;
            ctx.fill();
            ctx.strokeStyle = layer === 0 ? colors.darkCoffee : colors.coffee;
            ctx.lineWidth = 2 - layer * 0.3;
            ctx.stroke();

            ctx.restore();
        }
        
        function animate() {
            time += 0.008 * params.speed;
            
            const bgGradient = ctx.createRadialGradient(
                canvas.width/2, canvas.height/2, 0,
                canvas.width/2, canvas.height/2, canvas.width/2
            );
            bgGradient.addColorStop(0, colors.bg);
            bgGradient.addColorStop(1, colors.darkCoffee);
            
            ctx.fillStyle = bgGradient;
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Draw layers based on params
            for (let layer = 0; layer < params.layers; layer++) {
                const polygonCount = Math.min(params.polygonCount + layer * 2, 15);
                const angleStep = (Math.PI * 2) / polygonCount;
                const baseRadius = 100 * params.size;
                
                for (let i = 0; i < polygonCount; i++) {
                    const angle = i * angleStep + time * 0.3;
                    const orbitRadius = baseRadius * (1.2 + layer * 0.4);
                    const x = canvas.width/2 + Math.cos(angle) * orbitRadius;
                    const y = canvas.height/2 + Math.sin(angle) * orbitRadius;
                    
                    const sides = 6 + (i % 7);
                    const polygonRadius = (25 + layer * 8) * params.size;
                    const rotation = angle + time * 0.5;
                    const phase = time * 2 + i * 0.5;
                    
                    drawPolygon(x, y, polygonRadius, sides, rotation, phase, layer);
                }
            }
            
            requestAnimationFrame(animate);
        }
        
        animate();
    </script>
</body>
</html>
EOF
```

### Step 4: Create Wrapper Script
```bash
# Create wrapper script
cat > geometric-screensaver.sh << 'EOF'
#!/bin/bash
DISPLAY=${DISPLAY:-:0.0}
export DISPLAY

# Get screen dimensions
SCREEN_GEOMETRY=$(xdpyinfo | grep dimensions | awk '{print $2}')
WIDTH=$(echo $SCREEN_GEOMETRY | cut -d'x' -f1)
HEIGHT=$(echo $SCREEN_GEOMETRY | cut -d'x' -f2)

# Launch chromium in kiosk mode
exec chromium \
  --kiosk \
  --no-sandbox \
  --disable-gpu-sandbox \
  --disable-software-rasterizer \
  --disable-background-timer-throttling \
  --disable-backgrounding-occluded-windows \
  --disable-renderer-backgrounding \
  --disable-features=TranslateUI \
  --disable-extensions \
  --disable-plugins \
  --disable-sync \
  --disable-translate \
  --no-first-run \
  --window-size=$WIDTH,$HEIGHT \
  --window-position=0,0 \
  --app="file://$(pwd)/geometric-screensaver.html"
EOF

chmod +x geometric-screensaver.sh
```

### Step 5: Configure XScreenSaver
```bash
# Edit xscreensaver config
cat >> ~/.xscreensaver << 'EOF'

programs: \
  geometric-screensaver ~/.config/xscreensaver/hacks/geometric-screensaver.sh \n\

EOF
```

## Method 2: Standalone Electron App

### Create package.json
```json
{
  "name": "geometric-screensaver",
  "version": "1.0.0",
  "main": "main.js",
  "scripts": {
    "start": "electron ."
  },
  "devDependencies": {
    "electron": "^latest"
  }
}
```

### Create main.js
```javascript
const { app, BrowserWindow } = require('electron');
const path = require('path');

let mainWindow;

function createWindow() {
  mainWindow = new BrowserWindow({
    fullscreen: true,
    webPreferences: {
      nodeIntegration: true,
      contextIsolation: false
    },
    frame: false,
    show: false
  });

  mainWindow.loadFile('geometric-screensaver.html');
  
  mainWindow.once('ready-to-show', () => {
    mainWindow.show();
  });

  // Exit on any key press or mouse click
  mainWindow.webContents.on('before-input-event', () => {
    app.quit();
  });
}

app.whenReady().then(createWindow);

app.on('window-all-closed', () => {
  app.quit();
});
```

## Method 3: Native OpenGL (Advanced)

For maximum performance, you could port to C++ with OpenGL:

```bash
# Install development tools
sudo pacman -S base-devel cmake glfw-x11 glew
```

### Key Advantages of Each Method:

1. **HTML/XScreenSaver**: Easiest to implement, good performance, real-time controls
2. **Electron**: Full web APIs, slightly higher memory usage
3. **Native**: Maximum performance, more complex development

## Real-time Controls Implementation

For interactive controls, the HTML method gives you:
- Sliders for speed, polygon count, size, layers
- Keyboard shortcuts (add event listeners)
- Mouse interaction zones
- Auto-hiding controls
- Parameter saving to localStorage

## Recommended Next Steps:

1. Start with the HTML/XScreenSaver method
2. Convert your React canvas code to vanilla JavaScript
3. Add the interactive controls
4. Test with `xscreensaver-demo`
5. If performance isn't sufficient, consider the native approach

Would you like me to help you convert your specific React code to vanilla JavaScript for the HTML screensaver, or would you prefer to explore one of the native solutions?
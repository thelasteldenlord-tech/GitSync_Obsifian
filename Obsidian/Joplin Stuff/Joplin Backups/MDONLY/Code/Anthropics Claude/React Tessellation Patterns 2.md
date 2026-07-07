React Tessellation Patterns 2

```js

import React, { useEffect, useRef } from 'react';

const NierGeometricDesign = () => {
  const canvasRef = useRef(null);

  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas) return;

    const ctx = canvas.getContext('2d');
    const width = canvas.width = 600;
    const height = canvas.height = 600;
    let time = 0;
    let animationFrameId = null;

    // Nier Automata inspired color palette
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

      // Create gradient for cell shading effect
      const gradient = ctx.createRadialGradient(0, 0, 0, 0, 0, radius);
      
      // Different shading based on layer and phase
      const intensity = (Math.sin(phase) * 0.5 + 0.5);
      const shadowIntensity = (Math.cos(phase * 0.7) * 0.3 + 0.7);
      
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

      // Fill with gradient
      ctx.fillStyle = gradient;
      ctx.fill();

      // Add cell shading outline
      ctx.strokeStyle = layer === 0 ? colors.darkCoffee : colors.coffee;
      ctx.lineWidth = 2 - layer * 0.3;
      ctx.stroke();

      // Add inner geometric details
      if (sides >= 8) {
        ctx.beginPath();
        for (let i = 0; i < sides; i += 2) {
          const angle = (i / sides) * Math.PI * 2;
          const innerRadius = radius * 0.4;
          const x = Math.cos(angle) * innerRadius;
          const y = Math.sin(angle) * innerRadius;
          if (i === 0) {
            ctx.moveTo(x, y);
          } else {
            ctx.lineTo(x, y);
          }
        }
        ctx.strokeStyle = `rgba(75, 44, 23, ${shadowIntensity})`;
        ctx.lineWidth = 1;
        ctx.stroke();
      }

      ctx.restore();
    }

    function createGeometricLayer(centerX, centerY, baseRadius, timeOffset, layer) {
      const polygonCount = 6 + layer * 2;
      const angleStep = (Math.PI * 2) / polygonCount;
      
      for (let i = 0; i < polygonCount; i++) {
        const angle = i * angleStep + (time + timeOffset) * 0.3;
        const orbitRadius = baseRadius * (1.2 + layer * 0.4);
        const x = centerX + Math.cos(angle) * orbitRadius;
        const y = centerY + Math.sin(angle) * orbitRadius;
        
        const sides = 6 + (i % 7); // 6-12 sided polygons
        const polygonRadius = 25 + layer * 8;
        const rotation = angle + (time + timeOffset) * 0.5;
        const phase = (time + timeOffset) * 2 + i * 0.5;
        
        drawPolygon(x, y, polygonRadius, sides, rotation, phase, layer);
      }
    }

    function drawCentralPolygon() {
      const centerX = width / 2;
      const centerY = height / 2;
      const sides = 12;
      const radius = 60;
      const rotation = time * 0.4;
      const phase = time * 1.5;
      
      // Draw larger central polygon with special effects
      ctx.save();
      ctx.translate(centerX, centerY);
      ctx.rotate(rotation);
      
      // Create special gradient for center piece
      const centerGradient = ctx.createRadialGradient(0, 0, 0, 0, 0, radius);
      centerGradient.addColorStop(0, colors.lightCream);
      centerGradient.addColorStop(0.3, colors.accent);
      centerGradient.addColorStop(0.7, colors.coffee);
      centerGradient.addColorStop(1, colors.darkCoffee);
      
      ctx.beginPath();
      for (let i = 0; i <= sides; i++) {
        const angle = (i / sides) * Math.PI * 2;
        const r = radius * (1 + Math.sin(phase + i * 0.3) * 0.15);
        const x = Math.cos(angle) * r;
        const y = Math.sin(angle) * r;
        if (i === 0) {
          ctx.moveTo(x, y);
        } else {
          ctx.lineTo(x, y);
        }
      }
      
      ctx.fillStyle = centerGradient;
      ctx.fill();
      ctx.strokeStyle = colors.darkCoffee;
      ctx.lineWidth = 3;
      ctx.stroke();
      
      // Add inner star pattern
      ctx.beginPath();
      for (let i = 0; i < sides; i++) {
        const angle = (i / sides) * Math.PI * 2;
        const innerRadius = radius * 0.3;
        const outerRadius = radius * 0.6;
        const r = i % 2 === 0 ? outerRadius : innerRadius;
        const x = Math.cos(angle) * r;
        const y = Math.sin(angle) * r;
        if (i === 0) {
          ctx.moveTo(x, y);
        } else {
          ctx.lineTo(x, y);
        }
      }
      ctx.strokeStyle = colors.darkCoffee;
      ctx.lineWidth = 2;
      ctx.stroke();
      
      ctx.restore();
    }

    function animate() {
      time += 0.008;

      // Create subtle animated background
      const bgGradient = ctx.createRadialGradient(
        width/2, height/2, 0,
        width/2, height/2, width/2
      );
      bgGradient.addColorStop(0, colors.bg);
      bgGradient.addColorStop(1, colors.darkCoffee);
      
      ctx.fillStyle = bgGradient;
      ctx.fillRect(0, 0, width, height);

      const centerX = width / 2;
      const centerY = height / 2;

      // Draw multiple layers of rotating polygons
      createGeometricLayer(centerX, centerY, 80, 0, 2);
      createGeometricLayer(centerX, centerY, 60, Math.PI/3, 1);
      createGeometricLayer(centerX, centerY, 40, Math.PI/6, 0);
      
      // Draw the central focal polygon
      drawCentralPolygon();

      // Add floating accent polygons
      for (let i = 0; i < 8; i++) {
        const angle = (i / 8) * Math.PI * 2 + time * 0.2;
        const radius = 180 + Math.sin(time + i) * 20;
        const x = centerX + Math.cos(angle) * radius;
        const y = centerY + Math.sin(angle) * radius;
        const sides = 6 + (i % 4);
        const polygonRadius = 15 + Math.sin(time * 2 + i) * 5;
        const rotation = angle + time * 0.8;
        const phase = time * 3 + i;
        
        drawPolygon(x, y, polygonRadius, sides, rotation, phase, i % 3);
      }

      animationFrameId = requestAnimationFrame(animate);
    }

    animate();

    return () => {
      if (animationFrameId) {
        cancelAnimationFrame(animationFrameId);
        animationFrameId = null;
      }
      if (ctx) {
        ctx.clearRect(0, 0, width, height);
      }
      if (canvas) {
        canvas.width = 0;
        canvas.height = 0;
      }
    };
  }, []);

  return (
    <div style={{
      width: '600px',
      height: '600px',
      margin: 'auto',
      backgroundColor: '#2B2420',
      overflow: 'hidden',
      borderRadius: '8px',
      boxShadow: '0 8px 32px rgba(0,0,0,0.3)'
    }}>
      <canvas
        ref={canvasRef}
        style={{
          display: 'block',
          width: '600px',
          height: '600px'
        }}
      />
    </div>
  );
};

export default NierGeometricDesign;
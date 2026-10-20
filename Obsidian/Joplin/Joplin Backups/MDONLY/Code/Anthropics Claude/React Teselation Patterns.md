```js

import React, { useEffect, useRef } from 'react';

const TessellationPatterns = () => {
  const canvasRef = useRef(null);

  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas) return;

    const ctx = canvas.getContext('2d');
    const width = canvas.width = 550;
    const height = canvas.height = 550;
    let time = 0;
    const SCALE = 60;
    let animationFrameId = null;

    function drawTile(cx, cy, size, rotation, phase, morph) {
      ctx.save();
      ctx.translate(cx, cy);
      ctx.rotate(rotation);

      ctx.beginPath();
      const points = 6;
      for (let i = 0; i <= points; i++) {
        const angle = (i / points) * Math.PI * 2;
        const r = size * (1 + Math.sin(phase + i) * 0.1);
        const x = Math.cos(angle) * r;
        const y = Math.sin(angle) * r;
        if (i === 0) {
          ctx.moveTo(x, y);
        } else {
          ctx.lineTo(x, y);
        }
      }
      ctx.strokeStyle = 'rgba(51, 51, 51, 0.4)';
      ctx.lineWidth = 1;
      ctx.stroke();

      for (let i = 0; i < points; i += 2) {
        const angle1 = (i / points) * Math.PI * 2;
        const angle2 = ((i + 2) / points) * Math.PI * 2;
        const r1 = size * (1 + Math.sin(phase + i) * 0.1);
        const r2 = size * (1 + Math.sin(phase + i + 2) * 0.1);
        const x1 = Math.cos(angle1) * r1;
        const y1 = Math.sin(angle1) * r1;
        const x2 = Math.cos(angle2) * r2;
        const y2 = Math.sin(angle2) * r2;

        const midAngle = (angle1 + angle2) / 2;
        const innerR = size * 0.5 * (1 + morph * 0.5);
        const xi = Math.cos(midAngle) * innerR;
        const yi = Math.sin(midAngle) * innerR;

        ctx.beginPath();
        ctx.moveTo(x1, y1);
        ctx.lineTo(xi, yi);
        ctx.stroke();

        ctx.beginPath();
        ctx.moveTo(x2, y2);
        ctx.lineTo(xi, yi);
        ctx.stroke();
      }

      ctx.restore();
    }

    function createTessellationField(offsetX, offsetY, fieldScale, timeOffset) {
      const gridSize = 4;
      const spacing = SCALE * fieldScale * 0.8;

      for (let row = -gridSize; row <= gridSize; row++) {
        const rowOffset = (row % 2) * spacing * 0.5;
        for (let col = -gridSize; col <= gridSize; col++) {
          const x = (col * spacing * 0.866) + rowOffset + offsetX;
          const y = row * spacing * 0.75 + offsetY;
          const dist = Math.sqrt(x * x + y * y);

          if (dist > SCALE * fieldScale * 2.5) continue;

          const angle = Math.atan2(y - offsetY, x - offsetX);
          const phase = (time + timeOffset) + dist * 0.01;
          const morph = Math.sin(phase + angle) * 0.5 + 0.5;

          drawTile(
            width/2 + x,
            height/2 + y,
            SCALE * fieldScale * 0.4 * (1 - dist/(SCALE * fieldScale * 3) * 0.3),
            angle + (time + timeOffset) * 0.2,
            phase,
            morph
          );
        }
      }
    }

    function animate() {
      time += 0.01;

      ctx.fillStyle = '#F0EEE6';
      ctx.fillRect(0, 0, width, height);

      createTessellationField(0, 0, 1.5, 0);

      ctx.save();
      ctx.translate(width/2, height/2);
      ctx.rotate(Math.PI/6);
      ctx.translate(-width/2, -height/2);
      createTessellationField(0, -100, 0.8, time * 0.2 + Math.PI/3);
      ctx.restore();

      ctx.save();
      ctx.translate(width/2, height/2);
      ctx.rotate(-Math.PI/6);
      ctx.translate(-width/2, -height/2);
      createTessellationField(0, 100, 0.8, time * 0.2 - Math.PI/3);
      ctx.restore();

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
      width: '550px',
      height: '550px',
      margin: 'auto',
      backgroundColor: '#F0EEE6',
      overflow: 'hidden'
    }}>
      <canvas
        ref={canvasRef}
        style={{
          display: 'block',
          width: '550px',
          height: '550px'
        }}
      />
    </div>
  );
};

export default TessellationPatterns;
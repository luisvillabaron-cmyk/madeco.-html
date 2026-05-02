<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="mobile-web-app-capable" content="yes">
    <title>Madeco Villa - Protector de pantalla</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        html, body {
            width: 100%;
            height: 100%;
            overflow: hidden;
            background: #000;
            touch-action: none;
        }
        
        #canvas {
            display: block;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        
        @keyframes neonPulse {
            0%, 100% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); filter: blur(2px); }
            10%, 90% { opacity: 1; transform: translate(-50%, -50%) scale(1); filter: blur(0); }
        }
        
        .neon-text {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-family: 'Arial Black', Arial, sans-serif;
            font-size: clamp(28px, 8vw, 60px);
            font-weight: 900;
            text-align: center;
            color: #D4AF37;
            text-shadow:
                0 0 5px #D4AF37,
                0 0 10px #D4AF37,
                0 0 20px #D4AF37,
                0 0 40px #B87333,
                0 0 80px #B87333;
            letter-spacing: 4px;
            z-index: 20;
            pointer-events: none;
            opacity: 0;
        }
        
        .neon-text.show {
            animation: neonPulse 4s ease-in-out forwards;
        }
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>
    <div class="neon-text" id="neonLogo">MADECO<br>VILLA</div>

    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        const neonLogo = document.getElementById('neonLogo');
        let w, h, stars = [], nebulae = [];
        
        const dpr = window.devicePixelRatio || 1;
        
        function resize() {
            w = window.innerWidth;
            h = window.innerHeight;
            canvas.width = w * dpr;
            canvas.height = h * dpr;
            ctx.scale(dpr, dpr);
            initialize();
        }
        
        window.addEventListener('resize', resize);

        class Star {
            constructor() {
                this.reset();
                this.z = Math.random() * w;
            }
            reset() {
                this.x = Math.random() * w;
                this.y = Math.random() * h;
                this.z = w;
                this.size = Math.random() * 1.5;
                this.speed = Math.random() * 2 + 1;
                this.opacity = Math.random() * 0.5 + 0.3;
            }
            update() {
                this.z -= this.speed;
                if (this.z <= 0) this.reset();
                this.sx = (this.x - w / 2) * (w / this.z) + w / 2;
                this.sy = (this.y - h / 2) * (w / this.z) + h / 2;
                this.sSize = this.size * (w / this.z);
            }
            draw() {
                ctx.beginPath();
                ctx.fillStyle = `rgba(255, 255, 255, ${this.opacity})`;
                ctx.arc(this.sx, this.sy, this.sSize, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        function initialize() {
            stars = [];
            for(let i = 0; i < 400; i++) stars.push(new Star());
            
            // Mostrar el logo con un pequeño delay
            setTimeout(() => {
                neonLogo.classList.add('show');
            }, 1000);
        }

        function animate() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.2)';
            ctx.fillRect(0, 0, w, h);
            
            stars.forEach(star => {
                star.update();
                star.draw();
            });
            
            requestAnimationFrame(animate);
        }

        resize();
        animate();
    </script>
</body>
</html>

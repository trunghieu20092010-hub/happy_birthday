<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday Tôm</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            background-color: #000;
            overflow: hidden;
            font-family: 'Inter', 'Arial', sans-serif;
        }

        canvas {
            display: block;
        }

        #overlay {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            width: 100%;
            pointer-events: none;
        }

        .text {
            font-size: 5rem;
            font-weight: 900;
            color: #ffcc00; /* Màu vàng ngôi sao */
            text-shadow: 0 0 20px #ffcc00, 0 0 40px #ff9900;
            display: none;
            text-transform: uppercase;
            letter-spacing: 5px;
        }

        .final-msg {
            font-size: 2.5rem;
            color: #fff;
            display: none;
            margin-top: 20px;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.5); }
            to { opacity: 1; transform: scale(1); }
        }
    </style>
</head>
<body>
    <canvas id="starField"></canvas>
    <div id="overlay">
        <div id="t3" class="text">3</div>
        <div id="t2" class="text">2</div>
        <div id="t1" class="text">1</div>
        <div id="happy" class="text">HAPPY</div>
        <div id="birthday" class="text">BIRTHDAY</div>
        <div id="to" class="text">TO</div>
        <div id="tom" class="text">TÔM</div>
        <div id="final" class="final-msg">Chúc mừng sinh nhật cậu! ✨</div>
    </div>

    <script>
        const canvas = document.getElementById('starField');
        const ctx = canvas.getContext('2d');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const stars = [];
        const numStars = 100;

        // Khởi tạo ngôi sao
        for (let i = 0; i < numStars; i++) {
            stars.push({
                x: Math.random() * canvas.width,
                y: Math.random() * canvas.height,
                size: Math.random() * 20 + 10,
                speed: Math.random() * 3 + 2,
                opacity: Math.random()
            });
        }

        function drawStar(x, y, size) {
            ctx.fillStyle = "#ffcc00";
            ctx.beginPath();
            ctx.font = size + "px Arial";
            ctx.fillText("⭐", x, y);
            ctx.closePath();
        }

        function updateStars() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.1)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            for (let i = 0; i < stars.length; i++) {
                let s = stars[i];
                drawStar(s.x, s.y, s.size);
                
                s.y += s.speed;
                if (s.y > canvas.height) {
                    s.y = -20;
                    s.x = Math.random() * canvas.width;
                }
            }
            requestAnimationFrame(updateStars);
        }

        updateStars();

        // Trình tự hiển thị
        const sequence = ['t3', 't2', 't1', 'happy', 'birthday', 'to', 'tom', 'final'];
        let currentIndex = 0;

        function showNext() {
            if (currentIndex > 0) {
                document.getElementById(sequence[currentIndex - 1]).style.display = 'none';
            }
            if (currentIndex < sequence.length) {
                const el = document.getElementById(sequence[currentIndex]);
                el.style.display = 'block';
                el.style.animation = 'fadeIn 0.5s forwards';
                currentIndex++;
                
                // Điều chỉnh thời gian xuất hiện: 3-2-1 nhanh hơn, chữ chậm hơn
                let delay = (currentIndex <= 3) ? 800 : 1200;
                setTimeout(showNext, delay);
            }
        }

        window.onload = showNext;

        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    </script>
</body>
</html>

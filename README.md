# LLOYD-lucky-draw
로이드 럭키드로우
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lucky Draw</title>
    <style>
        body {
            margin: 0;
            font-family: 'Chalkboard SE', sans-serif;
            background-color: #f0f4eb;
        }
        .page {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            position: relative;
        }
        .hidden {
            display: none;
        }
        .page1 {
            background: url('images/first-image.jpg') no-repeat center center;
            background-size: contain;
        }
        .start-button {
            position: absolute;
            bottom: 50px;
            background-color: #cde2c9;
            border: 2px solid #b5d3a5;
            padding: 10px 20px;
            font-size: 20px;
            cursor: pointer;
            border-radius: 5px;
        }
        .countdown {
            font-size: 100px;
            color: #444;
        }
        .page2 {
            background: url('images/second-image.jpg') no-repeat center center;
            background-size: contain;
            position: relative;
            animation: shake 0.5s ease-in-out;
        }

        /* 빛나는 효과 (1번 효과) */
        .sparkle {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 20px;
            height: 20px;
            background-color: rgba(255, 215, 0, 0.7);
            border-radius: 50%;
            animation: sparkle-animation 1.5s ease-out forwards;
        }

        /* 빛나는 애니메이션 */
        @keyframes sparkle-animation {
            0% {
                transform: scale(1) translate(-50%, -50%);
                opacity: 1;
            }
            50% {
                transform: scale(2) translate(-50%, -50%);
                opacity: 0.8;
            }
            100% {
                transform: scale(1) translate(-50%, -50%);
                opacity: 0;
            }
        }

        /* 화면 흔들림 애니메이션 */
        @keyframes shake {
            0%, 100% {
                transform: translateX(0);
            }
            25% {
                transform: translateX(-10px);
            }
            50% {
                transform: translateX(10px);
            }
            75% {
                transform: translateX(-10px);
            }
        }

    </style>
</head>
<body>
    <!-- Page 1 -->
    <div class="page page1" id="page1">
        <button class="start-button" onclick="startLuckyDraw()">START!</button>
    </div>

    <!-- Countdown -->
    <div class="page hidden" id="countdown">
        <div class="countdown" id="count">3</div>
    </div>

    <!-- Page 2 -->
    <div class="page hidden page2" id="page2">
        <!-- 빛나는 효과 (1번 효과) -->
        <div class="sparkle"></div>
    </div>

    <script>
        function startLuckyDraw() {
            const page1 = document.getElementById('page1');
            const countdown = document.getElementById('countdown');
            const page2 = document.getElementById('page2');
            const count = document.getElementById('count');

            // Hide page 1
            page1.style.display = 'none';

            // Show countdown
            countdown.classList.remove('hidden');

            let counter = 3;
            const interval = setInterval(() => {
                count.textContent = counter;
                counter--;

                if (counter < 0) {
                    clearInterval(interval);
                    countdown.classList.add('hidden');

                    // Show page 2 with shake animation
                    page2.classList.remove('hidden');
                    page2.style.animation = 'shake 0.5s ease-in-out';

                    // 빛나는 효과 추가
                    createSparkles();
                }
            }, 500); // 0.5초 간격으로 변경되도록 설정
        }

        function createSparkles() {
            const page2 = document.getElementById('page2');

            // 빛나는 효과를 랜덤한 간격과 위치로 화면에 생성
            for (let i = 0; i < 5; i++) {
                const sparkle = document.createElement('div');
                sparkle.classList.add('sparkle');
                sparkle.style.top = `${Math.random() * 80 + 10}%`;  // 10%에서 90% 사이의 랜덤 위치
                sparkle.style.left = `${Math.random() * 80 + 10}%`; // 10%에서 90% 사이의 랜덤 위치
                sparkle.style.animationDelay = `${Math.random() * 1}s`; // 빛나는 타이밍을 랜덤으로 설정
                page2.appendChild(sparkle);

                // 애니메이션이 끝난 후 빛나는 효과를 제거
                setTimeout(() => {
                    sparkle.remove();
                }, 1500);
            }
        }
    </script>
</body>
</html>

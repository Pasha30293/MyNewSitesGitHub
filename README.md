# MyNewSitesGitHub
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Мой первый скрипт на GitHub</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #74ebd5, #acb6e5);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
            user-select: none;
        }
        h1 {
            color: #333;
            margin-bottom: 5px;
        }
        #score-board {
            font-size: 24px;
            font-weight: bold;
            color: #222;
            margin-bottom: 20px;
        }
        #game-zone {
            width: 90vw;
            height: 60vh;
            max-width: 600px;
            max-height: 400px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            position: relative;
            overflow: hidden;
            cursor: pointer;
        }
        #target {
            font-size: 40px;
            position: absolute;
            transition: all 0.2s ease;
            cursor: pointer;
            display: none;
        }
        #start-btn {
            padding: 12px 24px;
            font-size: 18px;
            background-color: #ff4757;
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(255, 71, 87, 0.4);
            transition: transform 0.1s;
        }
        #start-btn:active {
            transform: scale(0.95);
        }
    </style>
</head>
<body>

    <h1>Поймай Смайлик! 🎯</h1>
    <div id="score-board">Счет: <span id="score">0</span></div>
    
    <div id="game-zone">
        <div id="target">🎈</div>
    </div>
    
    <br>
    <button id="start-btn" onclick="startGame()">Начать игру</button>

    <script>
        const target = document.getElementById('target');
        const gameZone = document.getElementById('game-zone');
        const scoreDisplay = document.getElementById('score');
        const startBtn = document.getElementById('start-btn');
        
        let score = 0;
        let gameInterval;
        const emojis = ['🎈', '🦊', '⭐', '🍕', '🚀', '💎', '👻'];

        function moveTarget() {
            // Вычисляем случайные координаты внутри игровой зоны
            const maxX = gameZone.clientWidth - 50;
            const maxY = gameZone.clientHeight - 50;
            
            const randomX = Math.floor(Math.random() * maxX);
            const randomY = Math.floor(Math.random() * maxY);
            
            // Меняем смайлик на случайный
            const randomEmoji = emojis[Math.floor(Math.random() * emojis.length)];
            
            target.textContent = randomEmoji;
            target.style.left = randomX + 'px';
            target.style.top = randomY + 'px';
        }

        function startGame() {
            score = 0;
            scoreDisplay.textContent = score;
            startBtn.style.display = 'none';
            target.style.display = 'block';
            moveTarget();
            
            // Смайлик меняет позицию каждые 1.2 секунды, если по нему не кликнули
            clearInterval(gameInterval);
            gameInterval = setInterval(moveTarget, 1200);
        }

        // Обработчик клика по смайлику
        target.addEventListener('click', (e) => {
            e.stopPropagation(); // Предотвращаем клик по самой игровой зоне
            score++;
            scoreDisplay.textContent = score;
            moveTarget();
            
            // Сбрасываем таймер при успешном клике
            clearInterval(gameInterval);
            gameInterval = setInterval(moveTarget, 1200);
        });
    </script>
</body>
</html>

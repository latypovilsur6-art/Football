<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <title>Футбольное Табло</title>
  <style>
    body {
      margin: 0;
      background-color: transparent;
      font-family: Arial, sans-serif;
    }

    .container {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 10px;
    }

    .logo-timer {
      background-color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 0 10px;
      border-radius: 12px;
      height: 38px;
    }

    .logo {
      width: 22px;
      height: 22px;
      margin-right: 6px;
      cursor: pointer;
    }

    .timer {
      font-size: 15px;
      font-weight: bold;
      color: black;
      cursor: pointer;
    }

    .scoreboard-wrapper {
      display: flex;
      align-items: center;
      background-color: black;
      border-radius: 12px;
      height: 38px;
      padding: 0 10px;
    }

    .team-group {
      display: flex;
      align-items: center;
      height: 100%;
    }

    .color-bar {
      width: 6px;
      height: 20px;
      margin: 0 6px;
      border-radius: 3px;
      cursor: pointer;
    }

    .team {
      font-size: 15px;
      font-weight: bold;
      color: white;
      padding: 2px 6px;
      border-radius: 5px;
      cursor: pointer;
      white-space: nowrap;
    }

    .score-box {
      background-color: #ccc;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100%;
      border-radius: 0;
      padding: 0 6px;
      margin: 0 10px;
      min-width: 48px;
    }

    .score {
      background-color: transparent;
      color: black;
      padding: 2px 6px;
      font-size: 22px;
      font-weight: bold;
      margin: 0 4px;
      cursor: pointer;
      min-width: 20px;
      text-align: center;
    }

    .colon {
      color: black;
      font-size: 22px;
      font-weight: bold;
      padding: 0 4px;
    }

    input[type="file"] {
      display: none;
    }
  </style>
</head>
<body>

<div class="container">

  <!-- Белый блок логотипа и таймера -->
  <div class="logo-timer">
    <img src="" alt="Logo" class="logo" id="logo" />
    <input type="file" id="logoInput" accept="image/*" />
    <div class="timer" id="timer">00:00</div>
  </div>

  <!-- Чёрный блок со счётом и командами -->
  <div class="scoreboard-wrapper">

    <!-- Команда 1 -->
    <div class="team-group">
      <div class="color-bar" id="bar1" style="background-color: red;" onclick="cycleColor('bar1')"></div>
      <div class="team" id="team1" contenteditable="true">Команда 1</div>
    </div>

    <!-- Счёт -->
    <div class="score-box">
      <div class="score" id="score1">0</div>
      <div class="colon">:</div>
      <div class="score" id="score2">0</div>
    </div>

    <!-- Команда 2 -->
    <div class="team-group">
      <div class="team" id="team2" contenteditable="true">Команда 2</div>
      <div class="color-bar" id="bar2" style="background-color: blue;" onclick="cycleColor('bar2')"></div>
    </div>

  </div>
</div>

<!-- Скрипты -->
<script>
  let timerEl = document.getElementById('timer');
  let running = false;
  let time = 0;
  let interval = null;

  function updateTimer() {
    const minutes = String(Math.floor(time / 60)).padStart(2, '0');
    const seconds = String(time % 60).padStart(2, '0');
    timerEl.textContent = `${minutes}:${seconds}`;
  }

  timerEl.addEventListener('click', () => {
    if (!running) {
      interval = setInterval(() => {
        time++;
        updateTimer();
      }, 1000);
      running = true;
    } else {
      clearInterval(interval);
      running = false;
    }
  });

  const score1 = document.getElementById('score1');
  const score2 = document.getElementById('score2');

  score1.addEventListener('click', () => score1.textContent = +score1.textContent + 1);
  score2.addEventListener('click', () => score2.textContent = +score2.textContent + 1);

  score1.addEventListener('contextmenu', (e) => {
    e.preventDefault();
    score1.textContent = '0';
    score2.textContent = '0';
    time = 0;
    updateTimer();
  });

  score2.addEventListener('contextmenu', (e) => {
    e.preventDefault();
    score1.textContent = '0';
    score2.textContent = '0';
    time = 0;
    updateTimer();
  });

  // Цветовая смена по клику
  const colorSequence = ['red', 'blue', 'green', 'yellow', 'orange', 'purple', 'black', 'white'];

  function cycleColor(barId) {
    const bar = document.getElementById(barId);
    const currentColor = getComputedStyle(bar).backgroundColor;
    const hexColor = rgbToHex(currentColor);
    const index = colorSequence.findIndex(color => rgbToHex(color) === hexColor);
    const nextColor = colorSequence[(index + 1) % colorSequence.length];
    bar.style.backgroundColor = nextColor;
  }

  function rgbToHex(rgb) {
    if (rgb.startsWith('#')) return rgb.toLowerCase();

    const ctx = document.createElement('canvas').getContext('2d');
    ctx.fillStyle = rgb;
    return ctx.fillStyle.toLowerCase();
  }

  // Логотип
  const logo = document.getElementById('logo');
  const logoInput = document.getElementById('logoInput');
  logo.addEventListener('click', () => logoInput.click());
  logoInput.addEventListener('change', (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (event) => {
        logo.src = event.target.result;
      };
      reader.readAsDataURL(file);
    }
  });
</script>

</body>
</html>
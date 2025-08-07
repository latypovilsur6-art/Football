<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Футбольное Табло</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      background-color: #f5f5f5;
      padding: 20px;
    }
    h1 {
      margin-bottom: 30px;
    }
    .scoreboard {
      display: flex;
      justify-content: space-around;
      margin-bottom: 30px;
    }
    .team {
      font-size: 2em;
      padding: 20px;
      background-color: white;
      border-radius: 10px;
      cursor: pointer;
    }
    .bar {
      height: 10px;
      margin: 10px 0;
      background-color: #ccc;
      cursor: pointer;
    }
    #logo {
      width: 100px;
      height: auto;
      margin: 20px auto;
      display: block;
      cursor: pointer;
    }
  </style>
</head>
<body>

<h1>Футбольное Табло</h1>

<img id="logo" src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/1024px-React-icon.svg.png" alt="Логотип">

<div class="bar" id="bar1" onclick="showColorPicker('bar1', this)"></div>

<div class="scoreboard">
  <div class="team" id="score1">0</div>
  <div class="team" id="score2">0</div>
</div>

<div class="bar" id="bar2" onclick="showColorPicker('bar2', this)"></div>

<input type="file" id="logoInput" accept="image/*" style="display:none;">
<input type="color" id="colorPicker" style="position:absolute; left:-9999px;">

<script>
  const score1 = document.getElementById('score1');
  const score2 = document.getElementById('score2');

  score1.addEventListener('click', () => {
    score1.textContent = +score1.textContent + 1;
  });

  score2.addEventListener('click', () => {
    score2.textContent = +score2.textContent + 1;
  });

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

  const colorPicker = document.getElementById('colorPicker');
  function showColorPicker(barId, triggerEl) {
    const rect = triggerEl.getBoundingClientRect();
    colorPicker.style.position = 'fixed';
    colorPicker.style.left = rect.left + 'px';
    colorPicker.style.top = rect.bottom + 'px';
    colorPicker.style.zIndex = 1000;
    colorPicker.onchange = () => {
      document.getElementById(barId).style.backgroundColor = colorPicker.value;
      colorPicker.style.left = '-9999px';
    };
    colorPicker.onblur = () => {
      colorPicker.style.left = '-9999px';
    };
    colorPicker.click();
  }

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

  // Таймер
  let time = 0;
  function updateTimer() {
    // Можешь добавить отображение времени, если нужно
    console.log("Таймер сброшен: " + time + " сек.");
  }
</script>

</body>
</html>
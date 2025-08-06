<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>مؤقت التأمل</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f5f5f5;
      text-align: center;
      padding: 50px;
      direction: rtl;
    }

    h1 {
      color: #6a0dad;
      margin-bottom: 30px;
    }

    #countdown {
      font-size: 64px;
      margin: 40px 0;
      color: #333;
    }

    .buttons {
      display: flex;
      justify-content: center;
      gap: 20px;
      flex-wrap: wrap;
    }

    button {
      background-color: #6a0dad;
      color: white;
      border: none;
      padding: 15px 30px;
      font-size: 18px;
      border-radius: 12px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    button:hover {
      background-color: #5a0099;
    }

    @media (max-width: 600px) {
      #countdown {
        font-size: 40px;
      }

      button {
        padding: 10px 20px;
        font-size: 16px;
      }
    }
  </style>
</head>
<body>

  <h1>مؤقت التأمل</h1>
  <div id="countdown">30:00</div>

  <div class="buttons">
    <button onclick="startPauseTimer()">ابدأ / أوقف</button>
    <button onclick="resetTimer()">إعادة البدء</button>
  </div>

  <audio id="rainSound" loop>
    <source src="https://www.fesliyanstudios.com/play-mp3/387" type="audio/mpeg">
    متصفحك لا يدعم تشغيل الصوت.
  </audio>

  <script>
    let totalSeconds = 1800;
    let timer;
    let isRunning = false;

    const countdownEl = document.getElementById('countdown');
    const rainSound = document.getElementById('rainSound');

    function updateCountdown() {
      const minutes = Math.floor(totalSeconds / 60);
      const seconds = totalSeconds % 60;
      countdownEl.textContent = `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
      
      if (totalSeconds > 0) {
        totalSeconds--;
      } else {
        clearInterval(timer);
        isRunning = false;
        rainSound.pause();
        rainSound.currentTime = 0;
      }
    }

    function startPauseTimer() {
      if (!isRunning) {
        timer = setInterval(updateCountdown, 1000);
        isRunning = true;
        rainSound.play();
      } else {
        clearInterval(timer);
        isRunning = false;
        rainSound.pause();
      }
    }

    function resetTimer() {
      clearInterval(timer);
      isRunning = false;
      totalSeconds = 1800;
      updateCountdown();
      rainSound.pause();
      rainSound.currentTime = 0;
    }

    // Initialize with starting time
    updateCountdown();
  </script>
</body>
</html>

<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>مؤقت التأمل</title>
<style>
  body, html {
    height: 100%;
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: transparent;
  }
  .widget {
    width: 320px;
    height: 220px;
    background: linear-gradient(135deg, #c9a9ff, #6a0dad);
    border-radius: 15px;
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    user-select: none;
  }
  .title {
    font-size: 1.8rem;
    margin-bottom: 12px;
    font-weight: bold;
  }
  .timer {
    font-size: 2.8rem;
    font-weight: 700;
    margin-bottom: 15px;
    letter-spacing: 2px;
    font-family: monospace;
  }
  .buttons {
    display: flex;
    gap: 15px;
  }
  button {
    background: rgba(255, 255, 255, 0.3);
    border: none;
    border-radius: 8px;
    color: white;
    font-size: 1rem;
    padding: 8px 18px;
    cursor: pointer;
    transition: background 0.3s ease;
  }
  button:hover {
    background: rgba(255, 255, 255, 0.5);
  }
</style>
</head>
<body>
<div class="widget" role="region" aria-label="مؤقت التأمل">
  <div class="title">مؤقت التأمل</div>
  <div class="timer" id="timer">30:00</div>
  <div class="buttons">
    <button id="startPauseBtn">ابدأ</button>
    <button id="restartBtn">إعادة</button>
  </div>
</div>

<audio id="rainSound" loop>
  <source src="https://cdn.pixabay.com/audio/2022/09/22/audio_69e39bc33e.mp3" type="audio/mpeg" />
  متصفحك لا يدعم تشغيل الصوت.
</audio>

<script>
  const timerEl = document.getElementById('timer');
  const startPauseBtn = document.getElementById('startPauseBtn');
  const restartBtn = document.getElementById('restartBtn');
  const rainSound = document.getElementById('rainSound');

  const DURATION = 30 * 60; // 30 minutes
  let timeRemaining = DURATION;
  let timerInterval = null;
  let isRunning = false;

  function formatTime(seconds) {
    const mins = Math.floor(seconds / 60).toString().padStart(2, '0');
    const secs = (seconds % 60).toString().padStart(2, '0');
    return `${mins}:${secs}`;
  }

  function updateTimer() {
    timerEl.textContent = formatTime(timeRemaining);
  }

  function tick() {
    if (timeRemaining > 0) {
      timeRemaining--;
      updateTimer();
    } else {
      clearInterval(timerInterval);
      isRunning = false;
      startPauseBtn.textContent = "ابدأ";
      rainSound.pause();
      rainSound.currentTime = 0;
      alert("انتهى الوقت!");
    }
  }

  startPauseBtn.addEventListener('click', () => {
    if (!isRunning) {
      // Start or resume timer
      if (timeRemaining === 0) {
        timeRemaining = DURATION;
        updateTimer();
      }
      timerInterval = setInterval(tick, 1000);
      rainSound.play();
      isRunning = true;
      startPauseBtn.textContent = "إيقاف";
    } else {
      // Pause timer
      clearInterval(timerInterval);
      rainSound.pause();
      isRunning = false;
      startPauseBtn.textContent = "ابدأ";
    }
  });

  restartBtn.addEventListener('click', () => {
    clearInterval(timerInterval);
    timeRemaining = DURATION;
    updateTimer();
    rainSound.pause();
    rainSound.currentTime = 0;
    isRunning = false;
    startPauseBtn.textContent = "ابدأ";
  });

  // Initialize
  updateTimer();
</script>
</body>
</html>

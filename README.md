
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>مؤقت تأمل مع صوت المطر</title>
  <style>
    body {
      background: linear-gradient(to bottom right, #dbeafe, #f0f9ff);
      font-family: 'Cairo', sans-serif;
      text-align: center;
      padding: 40px;
      color: #1e293b;
    }
    h1 {
      font-size: 32px;
      margin-bottom: 20px;
    }
    #timer {
      font-size: 48px;
      margin: 20px 0;
    }
    button {
      background-color: #3b82f6;
      color: white;
      border: none;
      padding: 12px 24px;
      border-radius: 12px;
      font-size: 18px;
      cursor: pointer;
      margin: 10px;
      transition: 0.3s ease;
    }
    button:hover {
      background-color: #2563eb;
    }
    audio {
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <h1>مؤقت تأمل مع صوت المطر</h1>
  <div id="timer">05:00</div>
  <button onclick="startTimer()">ابدأ التأمل</button>
  <button onclick="resetTimer()">إعادة ضبط</button>

  <!-- صوت المطر -->
  <audio id="rainAudio" loop>
    <source src="https://cdn.pixabay.com/audio/2022/03/15/audio_c8048a1c51.mp3" type="audio/mpeg">
    متصفحك لا يدعم تشغيل الصوت.
  </audio>

  <script>
    let duration = 300; // 5 دقائق
    let remaining = duration;
    let timerInterval;

    function updateDisplay() {
      const minutes = Math.floor(remaining / 60).toString().padStart(2, '0');
      const seconds = (remaining % 60).toString().padStart(2, '0');
      document.getElementById('timer').textContent = `${minutes}:${seconds}`;
    }

    function startTimer() {
      clearInterval(timerInterval);
      const rainAudio = document.getElementById('rainAudio');
      rainAudio.volume = 0.4;
      rainAudio.play();
      timerInterval = setInterval(() => {
        remaining--;
        updateDisplay();
        if (remaining <= 0) {
          clearInterval(timerInterval);
          rainAudio.pause();
          rainAudio.currentTime = 0;
          alert('انتهى وقت التأمل 🌧️');
        }
      }, 1000);
    }

    function resetTimer() {
      clearInterval(timerInterval);
      remaining = duration;
      updateDisplay();
      const rainAudio = document.getElementById('rainAudio');
      rainAudio.pause();
      rainAudio.currentTime = 0;
    }

    updateDisplay();
  </script>
</body>
</html>

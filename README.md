<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>3D Alarm Clock</title>
  <style>
    body {
      margin: 0;
      background: #0f172a;
      font-family: sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      color: #fff;
      flex-direction: column;
    }

    .scene {
      width: 300px;
      height: 300px;
      perspective: 1000px;
    }

    .cube {
      width: 100%;
      height: 100%;
      position: relative;
      transform-style: preserve-3d;
      transform: rotateX(-20deg) rotateY(20deg);
      animation: rotate 20s linear infinite;
    }

    @keyframes rotate {
      from {
        transform: rotateX(-20deg) rotateY(0deg);
      }
      to {
        transform: rotateX(-20deg) rotateY(360deg);
      }
    }

    .face {
      position: absolute;
      width: 300px;
      height: 300px;
      background: #1e293b;
      border: 4px solid #475569;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2rem;
      box-shadow: 0 0 30px rgba(255, 255, 255, 0.1);
    }

    .front  { transform: translateZ(150px); }
    .back   { transform: rotateY(180deg) translateZ(150px); }
    .right  { transform: rotateY(90deg) translateZ(150px); }
    .left   { transform: rotateY(-90deg) translateZ(150px); }
    .top    { transform: rotateX(90deg) translateZ(150px); }
    .bottom { transform: rotateX(-90deg) translateZ(150px); }

    .controls {
      margin-top: 30px;
      display: flex;
      gap: 10px;
      flex-direction: column;
      align-items: center;
    }

    input[type="time"] {
      padding: 10px;
      font-size: 1rem;
      border-radius: 6px;
      border: none;
    }

    button {
      padding: 10px 20px;
      background-color: #0ea5e9;
      border: none;
      color: white;
      font-size: 1rem;
      border-radius: 6px;
      cursor: pointer;
    }

    button:hover {
      background-color: #0284c7;
    }
  </style>
</head>
<body>

  <div class="scene">
    <div class="cube" id="cube">
      <div class="face front" id="clock">--:--</div>
      <div class="face back">Alarm</div>
      <div class="face right">⏰</div>
      <div class="face left">🕒</div>
      <div class="face top">Time</div>
      <div class="face bottom">Set</div>
    </div>
  </div>

  <div class="controls">
    <input type="time" id="alarmTime">
    <button onclick="setAlarm()">Set Alarm</button>
  </div>

  <script>
    const clock = document.getElementById("clock");
    let alarm = null;

    function updateClock() {
      const now = new Date();
      const hrs = String(now.getHours()).padStart(2, "0");
      const mins = String(now.getMinutes()).padStart(2, "0");
      clock.textContent = `${hrs}:${mins}`;

      if (alarm === `${hrs}:${mins}`) {
        alert("⏰ Alarm Ringing!");
        alarm = null;
      }
    }

    function setAlarm() {
      const input = document.getElementById("alarmTime").value;
      if (input) {
        alarm = input;
        alert(`Alarm set for ${alarm}`);
      }
    }

    setInterval(updateClock, 1000);
    updateClock();
  </script>
</body>
</html>

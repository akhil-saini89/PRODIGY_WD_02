# PRODIGY_WD_02
This is a responsive and interactive Stopwatch Web Application built using HTML, CSS, and JavaScript. The app allows users to measure time intervals accurately with essential stopwatch features and a clean, visually engaging design.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Stopwatch App</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      background: #f0f8ff;
    }

    .half-circle {
      width: 200px;
      height: 100px;
      background: linear-gradient(to right, #007BFF, #00BFFF);
      border-top-left-radius: 100px;
      border-top-right-radius: 100px;
      margin-bottom: 20px;
    }

    .stopwatch {
      text-align: center;
    }

    .display {
      font-size: 48px;
      margin: 20px 0;
    }

    .buttons button {
      margin: 5px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      border: none;
      border-radius: 5px;
      background: linear-gradient(to right, #00bcd4, #2196f3);
      color: white;
      transition: background 0.3s;
    }

    .buttons button:hover {
      background: #007BFF;
    }

    ul {
      list-style: none;
      padding: 0;
      max-height: 150px;
      overflow-y: auto;
    }

    li {
      background: #e3f2fd;
      padding: 5px 10px;
      margin: 2px 0;
      border-radius: 5px;
    }
  </style>
</head>
<body>

  <div class="half-circle"></div>

  <div class="stopwatch">
    <h2>⏱ Stopwatch</h2>
    <div class="display" id="time">00:00:00</div>
    <div class="buttons">
      <button onclick="start()">Start</button>
      <button onclick="pause()">Pause</button>
      <button onclick="reset()">Reset</button>
      <button onclick="lap()">Lap</button>
    </div>
    <ul id="laps"></ul>
  </div>

  <script>
    let startTime = 0;
    let elapsed = 0;
    let interval = null;

    function updateDisplay() {
      const time = Date.now() - startTime + elapsed;
      const ms = Math.floor((time % 1000) / 10);
      const secs = Math.floor((time / 1000) % 60);
      const mins = Math.floor((time / 60000) % 60);
      document.getElementById("time").textContent =
        `${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}:${String(ms).padStart(2, '0')}`;
    }

    function start() {
      if (!interval) {
        startTime = Date.now();
        interval = setInterval(updateDisplay, 10);
      }
    }

    function pause() {
      if (interval) {
        clearInterval(interval);
        interval = null;
        elapsed += Date.now() - startTime;
      }
    }

    function reset() {
      clearInterval(interval);
      interval = null;
      startTime = 0;
      elapsed = 0;
      document.getElementById("time").textContent = "00:00:00";
      document.getElementById("laps").innerHTML = "";
    }

    function lap() {
      if (interval) {
        const lapTime = document.getElementById("time").textContent;
        const li = document.createElement("li");
        li.textContent = "Lap: " + lapTime;
        document.getElementById("laps").appendChild(li);
      }
    }
  </script>
</body>
</html>

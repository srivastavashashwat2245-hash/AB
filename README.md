<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Stopwatch App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #1e1e2f;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .container {
      text-align: center;
      background: #2c2c3e;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.3);
      width: 300px;
    }

    .time {
      font-size: 40px;
      margin-bottom: 20px;
    }

    button {
      padding: 10px 15px;
      margin: 5px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 14px;
      transition: 0.3s;
    }

    .start { background: #4caf50; color: white; }
    .pause { background: #ff9800; color: white; }
    .reset { background: #f44336; color: white; }
    .lap { background: #2196f3; color: white; }

    button:hover {
      opacity: 0.8;
    }

    ul {
      list-style: none;
      margin-top: 20px;
      padding: 0;
      max-height: 150px;
      overflow-y: auto;
    }

    ul li {
      padding: 5px;
      border-bottom: 1px solid #444;
      font-size: 14px;
    }
  </style>
</head>
<body>

  <div class="container">
    <h2>Stopwatch</h2>
    <div class="time" id="display">00:00:00</div>

    <button class="start" onclick="start()">Start</button>
    <button class="pause" onclick="pause()">Pause</button>
    <button class="reset" onclick="reset()">Reset</button>
    <button class="lap" onclick="lap()">Lap</button>

    <ul id="laps"></ul>
  </div>

  <script>
    let startTime = 0;
    let elapsedTime = 0;
    let timerInterval;
    let running = false;

    function timeToString(time) {
      let hrs = Math.floor(time / 3600000);
      let mins = Math.floor((time % 3600000) / 60000);
      let secs = Math.floor((time % 60000) / 1000);

      return (
        String(hrs).padStart(2, '0') + ":" +
        String(mins).padStart(2, '0') + ":" +
        String(secs).padStart(2, '0')
      );
    }

    function start() {
      if (!running) {
        startTime = Date.now() - elapsedTime;
        timerInterval = setInterval(() => {
          elapsedTime = Date.now() - startTime;
          document.getElementById("display").textContent = timeToString(elapsedTime);
        }, 1000);
        running = true;
      }
    }

    function pause() {
      clearInterval(timerInterval);
      running = false;
    }

    function reset() {
      clearInterval(timerInterval);
      document.getElementById("display").textContent = "00:00:00";
      elapsedTime = 0;
      running = false;
      document.getElementById("laps").innerHTML = "";
    }

    function lap() {
      if (running) {
        const lapTime = document.getElementById("display").textContent;
        const li = document.createElement("li");
        li.textContent = "Lap: " + lapTime;
        document.getElementById("laps").appendChild(li);
      }
    }
  </script>

</body>
</html>

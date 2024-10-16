<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Stopwatch</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
    }

    .container {
      text-align: center;
      background-color: #fff;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
    }

    h1 {
      margin-bottom: 20px;
    }

    #display {
      font-size: 48px;
      margin-bottom: 20px;
    }

    .buttons button {
      font-size: 16px;
      padding: 10px 20px;
      margin: 0 10px;
      cursor: pointer;
      border: none;
      background-color: #4CAF50;
      color: white;
      border-radius: 5px;
    }

    .buttons button:hover {
      background-color: #45a049;
    }

    .buttons button:disabled {
      background-color: #ccc;
      cursor: not-allowed;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Stopwatch</h1>
    <div id="display">00:00:00</div>
    <div class="buttons">
      <button id="startBtn">Start</button>
      <button id="stopBtn">Stop</button>
      <button id="resetBtn">Reset</button>
    </div>
  </div>

  <script>
    let [milliseconds, seconds, minutes] = [0, 0, 0];
    let timerRef = document.getElementById('display');
    let interval = null;

    document.getElementById('startBtn').addEventListener('click', start);
    document.getElementById('stopBtn').addEventListener('click', stop);
    document.getElementById('resetBtn').addEventListener('click', reset);

    function start() {
      if (interval !== null) {
        clearInterval(interval);
      }
      interval = setInterval(displayTimer, 10);
    }

    function stop() {
      clearInterval(interval);
    }

    function reset() {
      clearInterval(interval);
      [milliseconds, seconds, minutes] = [0, 0, 0];
      timerRef.innerHTML = '00:00:00';
    }

    function displayTimer() {
      milliseconds += 10;
      if (milliseconds == 1000) {
        milliseconds = 0;
        seconds++;
        if (seconds == 60) {
          seconds = 0;
          minutes++;
        }
      }

      let m = minutes < 10 ? '0' + minutes : minutes;
      let s = seconds < 10 ? '0' + seconds : seconds;
      let ms = milliseconds < 10 ? '00' + milliseconds : milliseconds < 100 ? '0' + milliseconds : milliseconds;

      timerRef.innerHTML = `${m}:${s}:${ms}`;
    }
  </script>
</body>
</html>

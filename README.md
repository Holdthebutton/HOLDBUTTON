<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hold the Button Game</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background-color: #f0f0f0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            user-select: none; /* Prevent all text selection */
        }

        .game-container {
            text-align: center;
            padding: 20px;
            background-color: #ffffff;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
            width: 90%;
            max-width: 400px;
        }

        h1 {
            font-size: 24px;
            margin-bottom: 20px;
        }

        .instructions p {
            font-size: 18px;
            margin-bottom: 20px;
        }

        .button {
            background-color: #4CAF50;
            color: white;
            padding: 20px;
            font-size: 20px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .button:active {
            background-color: #45a049;
        }

        .result {
            margin-top: 20px;
        }

        .result p {
            font-size: 16px;
        }

        @media (max-width: 500px) {
            .button {
                font-size: 18px;
                padding: 15px;
            }
        }

        #currentTime {
            display: none;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>Hold the Button for Exactly 10 Seconds!</h1>
        <div class="instructions">
            <p>Press and hold the button for 10 seconds.</p>
        </div>
        <button id="holdButton" class="button">Hold Me!</button>
        <div class="result">
            <p>Closest Time: <span id="closestTime">0.00</span> seconds</p>
            <p>Current Time: <span id="currentTime">0.00</span> seconds</p>
        </div>
    </div>

    <script>
        let holdButton = document.getElementById("holdButton");
        let currentTimeSpan = document.getElementById("currentTime");
        let closestTimeSpan = document.getElementById("closestTime");

        let closestTime = 0;
        let startTime = 0;
        let holding = false;

        let interval;

        function updateCurrentTime() {
            if (holding) {
                let elapsedTime = (Date.now() - startTime) / 1000;
            }
        }

        function checkResult() {
            let elapsedTime = (Date.now() - startTime) / 1000;
            if (Math.abs(elapsedTime - 10) < Math.abs(closestTime - 10)) {
                closestTime = elapsedTime;
                closestTimeSpan.innerText = closestTime.toFixed(2);
            }
        }

        holdButton.addEventListener("touchstart", startHold);
        holdButton.addEventListener("mousedown", startHold);

        holdButton.addEventListener("touchend", stopHold);
        holdButton.addEventListener("mouseup", stopHold);

        function startHold() {
            holding = true;
            startTime = Date.now();
            interval = setInterval(updateCurrentTime, 10);
        }

        function stopHold() {
            if (holding) {
                holding = false;
                clearInterval(interval);
                checkResult();
            }
        }
    </script>
</body>
</html>

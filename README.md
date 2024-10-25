<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cookie Clicker with Upgrades and Achievements</title>
    <style>
        body {
            text-align: center;
            font-family: 'Arial', sans-serif;
        }

        #cookie {
            width: 200px;
            height: 200px;
            margin-top: 50px;
            cursor: pointer;
        }

        #score {
            font-size: 24px;
            margin-top: 20px;
        }

        .upgrade {
            margin: 10px;
            padding: 5px 10px;
            font-size: 16px;
            cursor: pointer;
        }

        .achievement {
            margin: 10px;
            font-size: 16px;
        }
    </style>
</head>
<body>

    <h1>Cookie Clicker with Upgrades and Achievements</h1>
    
    <img id="cookie" src="cookie.png" alt="Cookie" onclick="clickCookie()">
    <p id="score">Score: <span id="scoreValue">0</span></p>

    <h2>Upgrades</h2>
    <p id="clickValue">Click Value: 1</p>
    
    <button class="upgrade" onclick="buyUpgrade(10, 2)">Upgrade 1 (Cost: 10 cookies)</button>
    <button class="upgrade" onclick="buyUpgrade(20, 4)">Upgrade 2 (Cost: 20 cookies)</button>

    <h2>Auto-Clicker</h2>
    <p id="autoClickerStatus">Auto-Clicker: Off</p>
    <button class="upgrade" onclick="buyAutoClicker(50, 1)">Buy Auto-Clicker (Cost: 50 cookies)</button>
    <button class="upgrade" onclick="buyUpgradeAutoClicker(30, 1)">Upgrade Auto-Clicker (Cost: 30 cookies)</button>

    <h2>Achievements</h2>
    <p class="achievement" id="achievement1">Achievement 1: Not yet achieved</p>
    <p class="achievement" id="achievement2">Achievement 2: Not yet achieved</p>
    <!-- Add more achievements as needed -->

    <script>
        // JavaScript code for the cookie clicker game with upgrades, auto-clicker, and achievements
        var score = 0;
        var clickValue = 1;
        var autoClickerEnabled = false;
        var autoClickerInterval;
        var upgradeCount = 0;
        var cookiesAchievementThreshold = 100;
        var upgradesAchievementThreshold = 5;
        var autoClickerAchievementThreshold = 1;

        function clickCookie() {
            score += clickValue;
            updateScore();

            // Check and update achievements
            checkAchievements();
        }

        function updateScore() {
            document.getElementById("scoreValue").innerText = score;
        }

        function updateClickValue() {
            document.getElementById("clickValue").innerText = "Click Value: " + clickValue;
        }

        function updateAchievement(achievementId, message) {
            document.getElementById(achievementId).innerText = message;
        }

        function buyUpgrade(cost, increase) {
            if (score >= cost) {
                score -= cost;
                clickValue += increase;
                upgradeCount++;
                updateScore();
                updateClickValue();

                // Check and update achievements
                checkAchievements();
            } else {
                alert("Not enough cookies to buy this upgrade!");
            }
        }

        function buyAutoClicker(cost, initialSpeed) {
            if (score >= cost && !autoClickerEnabled) {
                score -= cost;
                autoClickerEnabled = true;
                document.getElementById("autoClickerStatus").innerText = "Auto-Clicker: On";
                autoClickerInterval = setInterval(autoClick, 1000 / initialSpeed);
                
                // Check and update achievements
                checkAchievements();
            } else if (autoClickerEnabled) {
                alert("Auto-Clicker is already enabled!");
            } else {
                alert("Not enough cookies to buy the Auto-Clicker!");
            }
        }

        function buyUpgradeAutoClicker(cost, speedIncrease) {
            if (score >= cost && autoClickerEnabled) {
                score -= cost;
                clearInterval(autoClickerInterval);
                autoClickerInterval = setInterval(autoClick, 1000 / (1 + speedIncrease));
                
                // Check and update achievements
                checkAchievements();
            } else {
                alert("Either Auto-Clicker is not enabled, or not enough cookies to buy this upgrade!");
            }
        }

        function autoClick() {
            score += clickValue;
            updateScore();
        }

        function checkAchievements() {
            // Check and update achievements based on thresholds
            if (score >= cookiesAchievementThreshold) {
                updateAchievement("achievement1", "Achievement 1: Unlocked!");
            }

            if (upgradeCount >= upgradesAchievementThreshold) {
                updateAchievement("achievement2", "Achievement 2: Unlocked!");
            }

            if (autoClickerEnabled && score >= autoClickerAchievementThreshold) {
                // Add more achievements as needed for other thresholds
            }
        }
    </script>

</body>
</html>

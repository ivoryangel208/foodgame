<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cultivate: The Weed Empire</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .container {
            width: 80%;
            margin: 20px;
            padding: 20px;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        h1, h2, p {
            text-align: center;
        }

        .button {
            background-color: #4CAF50;
            color: white;
            padding: 15px 20px;
            margin: 5px;
            border: none;
            cursor: pointer;
            font-size: 16px;
            border-radius: 5px;
        }

        .button:hover {
            background-color: #45a049;
        }

        .inventory, .store, .achievements, .goal-list {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 10px;
        }

        .inventory-item {
            margin: 5px;
            padding: 5px;
            background-color: #f0f0f0;
            border-radius: 5px;
            width: 200px;
            text-align: center;
        }

        .alert {
            color: red;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Cultivate: The Weed Empire</h1>
        <p id="cash">Cash: $0</p>
        <div class="button-container">
            <button class="button" onclick="buySeed()">Buy Seed ($100)</button>
            <button class="button" onclick="buyMysteryBox()">Buy Mystery Box ($500)</button>
            <button class="button" onclick="saveGame()">Save Game</button>
            <button class="button" onclick="loadGame()">Load Game</button>
        </div>

        <h2>Plants:</h2>
        <div id="plant-status"></div>

        <h2>Inventory:</h2>
        <div id="inventory"></div>

        <h2>Achievements:</h2>
        <div id="achievements"></div>

        <h2>Goals:</h2>
        <div id="goal-list"></div>

        <h2>Store:</h2>
        <div class="store">
            <button class="button" onclick="buySpecialSeed()">Buy Special Seed ($1000)</button>
            <button class="button" onclick="buyGrowBooster()">Buy Grow Booster ($200)</button>
        </div>

        <h2>Mystery Box:</h2>
        <div class="store">
            <button class="button" onclick="buyMysteryBox()">Buy Mystery Box ($500)</button>
        </div>
    </div>

    <script>
        let cash = 0;
        let inventory = [];
        let achievements = [];
        let goals = [
            { goal: "Earn $10,000", achieved: false },
            { goal: "Grow 5 Plants", achieved: false }
        ];

        // Strains data (including real names, percentages, origin, rarity)
        const strains = [
            { name: "Blue Dream", potency: 21, origin: "California", rarity: "Common", price: 200 },
            { name: "OG Kush", potency: 25, origin: "California", rarity: "Rare", price: 300 },
            { name: "Girl Scout Cookies", potency: 18, origin: "California", rarity: "Common", price: 250 },
            { name: "Northern Lights", potency: 30, origin: "Afghanistan", rarity: "Rare", price: 400 },
            { name: "Sour Diesel", potency: 22, origin: "New York", rarity: "Uncommon", price: 350 }
        ];

        // Game functions
        function updateUI() {
            document.getElementById("cash").innerText = "Cash: $" + cash;
            updateInventory();
            updateAchievements();
            updateGoals();
            checkAchievements();
            checkGoals();
        }

        function buySeed() {
            if (cash >= 100) {
                cash -= 100;
                let strain = strains[Math.floor(Math.random() * strains.length)];
                inventory.push(strain);
                alert("You bought a seed: " + strain.name);
                updateUI();
            } else {
                alert("Not enough cash!");
            }
        }

        function buyMysteryBox() {
            if (cash >= 500) {
                cash -= 500;
                alert("You opened a Mystery Box!");
                let item = generateRandomItem();
                inventory.push(item);
                updateUI();
            } else {
                alert("Not enough cash!");
            }
        }

        function buySpecialSeed() {
            if (cash >= 1000) {
                cash -= 1000;
                alert("You bought a Special Seed!");
                let strain = strains[Math.floor(Math.random() * strains.length)];
                inventory.push(strain);
                updateUI();
            } else {
                alert("Not enough cash!");
            }
        }

        function generateRandomItem() {
            const items = ['Super Fertilizer', 'Rare Seed', 'Instant Growth', 'Cash Boost'];
            let randomItem = items[Math.floor(Math.random() * items.length)];
            return randomItem;
        }

        function buyGrowBooster() {
            if (cash >= 200) {
                cash -= 200;
                alert("You bought a Grow Booster!");
                updateUI();
            } else {
                alert("Not enough cash!");
            }
        }

        function updateInventory() {
            let inventoryDiv = document.getElementById("inventory");
            inventoryDiv.innerHTML = "";
            inventory.forEach(item => {
                let div = document.createElement("div");
                div.className = "inventory-item";
                if (typeof item === "string") {
                    div.innerText = item; // Non-strain item like fertilizer
                } else {
                    div.innerText = item.name + " (Potency: " + item.potency + "%) - " + item.origin + " - " + item.rarity + " - $" + item.price;
                }
                inventoryDiv.appendChild(div);
            });
        }

        function updateAchievements() {
            let achievementsDiv = document.getElementById("achievements");
            achievementsDiv.innerHTML = achievements.length === 0 ? "No achievements unlocked yet" : achievements.join(", ");
        }

        function updateGoals() {
            let goalListDiv = document.getElementById("goal-list");
            goalListDiv.innerHTML = "";
            goals.forEach(goal => {
                let div = document.createElement("div");
                div.innerText = goal.goal + (goal.achieved ? " - Completed!" : " - In Progress");
                goalListDiv.appendChild(div);
            });
        }

        function checkAchievements() {
            if (cash >= 1000 && !achievements.includes("Earn $1000")) {
                achievements.push("Earn $1000");
                alert("Achievement Unlocked: Earn $1000!");
            }

            if (inventory.length >= 5 && !achievements.includes("Grow 5 Plants")) {
                achievements.push("Grow 5 Plants");
                alert("Achievement Unlocked: Grow 5 Plants!");
            }
        }

        function checkGoals() {
            if (cash >= 10000 && !goals[0].achieved) {
                goals[0].achieved = true;
                alert("Goal Achieved: Earn $10,000!");
            }

            if (inventory.length >= 5 && !goals[1].achieved) {
                goals[1].achieved = true;
                alert("Goal Achieved: Grow 5 Plants!");
            }
        }

        function saveGame() {
            localStorage.setItem("cash", cash);
            localStorage.setItem("inventory", JSON.stringify(inventory));
            localStorage.setItem("achievements", JSON.stringify(achievements));
            localStorage.setItem("goals", JSON.stringify(goals));
            alert("Game saved!");
        }

        function loadGame() {
            if(localStorage.getItem("cash") && localStorage.getItem("inventory")) {
                cash = parseInt(localStorage.getItem("cash"));
                inventory = JSON.parse(localStorage.getItem("inventory"));
                achievements = JSON.parse(localStorage.getItem("achievements"));
                goals = JSON.parse(localStorage.getItem("goals"));
                updateUI();
                alert("Game loaded!");
            }
        }

        // Initialize the game
        loadGame();
        setInterval(() => {
            // Random event or growth updates
            // You can trigger random events like Rain, Pest, etc. based on time intervals here.
        }, 10000); // every 10 seconds for example
    </script>
</body>
</html>

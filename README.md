<!DOCTYPE html>
<html>
<head>
    <title>Cooking & Fishing Adventure</title>
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            transition: background-color 0.5s;
        }
        .game-container {
            margin-top: 20px;
        }
        .button {
            font-size: 20px;
            padding: 10px;
            margin: 10px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: transform 0.2s, background-color 0.3s;
        }
        .button:hover {
            transform: scale(1.1);
        }
        .inventory {
            margin-top: 20px;
            padding: 10px;
            border: 2px solid black;
            background: white;
            font-size: 18px;
            text-align: left;
            width: 300px;
        }
        .inventory-section {
            margin-top: 10px;
            cursor: pointer;
            font-weight: bold;
            background-color: #ddd;
            padding: 5px;
            border-radius: 5px;
        }
        .inventory-content {
            display: none;
            padding-left: 10px;
        }
    </style>
</head>
<body>
    <h1>Cooking & Fishing Adventure</h1>
    <p>Catch fish, grow crops, cook meals, and explore the world!</p>

    <div class="game-container">
        <button class="button fish-btn" onclick="goFishing(); changeBackground('#2196F3')">🎣 Fish</button>
        <button class="button cook-btn" onclick="cookFood(); changeBackground('#ff9800')">🍳 Cook</button>
        <button class="button sell-btn" onclick="sellFood(); changeBackground('#4CAF50')">💰 Sell Food</button>
        <button class="button buy-btn" onclick="buyUpgrade(); changeBackground('#9C27B0')">🛒 Buy Upgrade</button>
        <button class="button farm-btn" onclick="plantCrop(); changeBackground('#8BC34A')">🌱 Plant Crop</button>
        <button class="button harvest-btn" onclick="harvestCrops(); changeBackground('#FFD700')">🌾 Harvest Crops</button>
        <button class="button travel-btn" onclick="travel(); changeBackground('#FF5722')">🚗 Travel</button>
    </div>

    <div class="inventory">
        <h3>Inventory</h3>
        <p>Coins: 💰 <span id="coins">0</span></p>
        <p>Fishing Level: 🎣 <span id="fishingLevel">1</span></p>
        
        <div class="inventory-section" onclick="toggleInventory('fishContent')">Fish Caught</div>
        <div id="fishContent" class="inventory-content">
            <ul id="fishList"></ul>
        </div>

        <div class="inventory-section" onclick="toggleInventory('mealContent')">Meals Cooked</div>
        <div id="mealContent" class="inventory-content">
            <ul id="mealList"></ul>
        </div>

        <div class="inventory-section" onclick="toggleInventory('cropContent')">Crops Harvested</div>
        <div id="cropContent" class="inventory-content">
            <ul id="cropList"></ul>
        </div>
    </div>

    <script>
        let fishInventory = [];
        let mealInventory = [];
        let cropInventory = [];
        let coins = 0;
        let fishingLevel = 1;

        function changeBackground(color) {
            document.body.style.backgroundColor = color;
        }

        function goFishing() {
            let fishTypes = [
                { name: "Salmon", weight: "5 lbs", length: "24 inches", rarity: "Common", description: "A fresh wild salmon." },
                { name: "Tuna", weight: "10 lbs", length: "40 inches", rarity: "Uncommon", description: "A powerful deep-sea fish." },
                { name: "Golden Koi", weight: "2 lbs", length: "14 inches", rarity: "Rare", description: "A stunning, valuable fish." },
                { name: "Swordfish", weight: "20 lbs", length: "60 inches", rarity: "Epic", description: "A mighty ocean predator." }
            ];
            let caughtFish = fishTypes[Math.floor(Math.random() * fishTypes.length)];
            fishInventory.push(caughtFish);
            updateInventory();
        }

        function cookFood() {
            if (fishInventory.length > 0) {
                let meal = { name: "Grilled Fish", description: "A delicious grilled fish." };
                mealInventory.push(meal);
                fishInventory.pop();
                updateInventory();
            } else {
                alert("You need more fish to cook!");
            }
        }

        function sellFood() {
            let earnings = mealInventory.length * 5 + cropInventory.length * 3;
            coins += earnings;
            mealInventory = [];
            cropInventory = [];
            updateInventory();
        }

        function buyUpgrade() {
            if (coins >= 20) {
                coins -= 20;
                fishingLevel++;
                alert("You upgraded your fishing gear! Catch more fish!");
                updateInventory();
            } else {
                alert("Not enough coins for an upgrade!");
            }
        }

        function plantCrop() {
            setTimeout(() => {
                let crop = { name: "Carrot", description: "A fresh organic carrot." };
                cropInventory.push(crop);
                alert("Your crops are ready to harvest!");
                updateInventory();
            }, 5000);
        }

        function harvestCrops() {
            if (cropInventory.length > 0) {
                alert("You harvested your crops!");
                updateInventory();
            } else {
                alert("No crops to harvest!");
            }
        }

        function travel() {
            alert("You traveled to a new location!");
        }

        function toggleInventory(id) {
            let element = document.getElementById(id);
            element.style.display = element.style.display === "block" ? "none" : "block";
        }

        function updateInventory() {
            document.getElementById('coins').textContent = coins;
            document.getElementById('fishingLevel').textContent = fishingLevel;
            document.getElementById('fishList').innerHTML = fishInventory.map(f => `<li>${f.name} (${f.rarity}) - ${f.weight}, ${f.length}: ${f.description}</li>`).join('');
            document.getElementById('mealList').innerHTML = mealInventory.map(m => `<li>${m.name}: ${m.description}</li>`).join('');
            document.getElementById('cropList').innerHTML = cropInventory.map(c => `<li>${c.name}: ${c.description}</li>`).join('');
        }
    </script>
</body>
</html>


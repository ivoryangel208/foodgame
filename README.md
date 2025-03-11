<!DOCTYPE html>
<html>
<head>
    <title>Cooking & Fishing Adventure</title>
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
        }
        .game-container {
            margin-top: 20px;
        }
        .button {
            font-size: 18px;
            padding: 10px;
            margin: 10px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
        }
        .inventory, .store, .fish-tank {
            margin-top: 20px;
            padding: 10px;
            border: 2px solid black;
            background: white;
            font-size: 18px;
            text-align: left;
            width: 300px;
            display: inline-block;
        }
        .hidden { display: none; }
    </style>
</head>
<body>
    <h1>Cooking & Fishing Adventure</h1>
    <p>Catch fish, grow crops, cook meals, and explore the world!</p>

    <div class="game-container">
        <button class="button" onclick="goFishing()">🎣 Fish</button>
        <button class="button" onclick="cookFood()">🍳 Cook</button>
        <button class="button" onclick="sellFood()">💰 Sell Food</button>
        <button class="button" onclick="openStore()">🛒 Open Store</button>
        <button class="button" onclick="plantCrop()">🌱 Plant Crop</button>
        <button class="button" onclick="harvestCrops()">🌾 Harvest Crops</button>
        <button class="button" onclick="openFishTank()">🐟 Fish Tank</button>
    </div>

    <div class="inventory">
        <h3>Inventory</h3>
        <p>Coins: 💰 <span id="coins">0</span></p>
        <p>Fishing Level: 🎣 <span id="fishingLevel">1</span></p>
        <ul id="inventoryList"></ul>
    </div>

    <div class="store hidden">
        <h3>Store</h3>
        <button class="button" onclick="buyItem('Rod')">🎣 Buy Better Rod (20 coins)</button>
        <button class="button" onclick="buyItem('Bait')">🪱 Buy Bait (5 coins)</button>
        <button class="button" onclick="buyItem('Seeds')">🌱 Buy Seeds (3 coins)</button>
        <button class="button" onclick="closeStore()">❌ Close</button>
    </div>

    <div class="fish-tank hidden">
        <h3>Fish Tank</h3>
        <ul id="fishTankList"></ul>
        <button class="button" onclick="closeFishTank()">❌ Close</button>
    </div>

    <script>
        let fishInventory = [];
        let mealInventory = [];
        let cropInventory = [];
        let fishTank = [];
        let coins = 0;
        let fishingLevel = 1;
        let storeOpen = false;
        let fishTypes = [
            { name: "Salmon", rarity: "Common", value: 5 },
            { name: "Tuna", rarity: "Uncommon", value: 10 },
            { name: "Golden Koi", rarity: "Rare", value: 20 },
            { name: "Swordfish", rarity: "Epic", value: 30 }
        ];
        let recipes = {
            "Salmon+Tuna": "Grilled Fish Combo",
            "Tuna+Golden Koi": "Exotic Seafood Platter"
        };
        let recipeBook = [];

        function goFishing() {
            let luckBoost = fishingLevel * 0.05;
            let fish = fishTypes[Math.floor(Math.random() * fishTypes.length)];
            if (Math.random() < luckBoost) {
                fish = fishTypes.find(f => f.rarity === "Rare") || fish;
            }
            fishInventory.push(fish);
            updateInventory();
        }

        function cookFood() {
            if (fishInventory.length >= 2) {
                let fish1 = fishInventory.pop();
                let fish2 = fishInventory.pop();
                let mealName = recipes[fish1.name + "+" + fish2.name] || "Mystery Dish";
                mealInventory.push({ name: mealName });
                if (!recipeBook.includes(mealName)) {
                    recipeBook.push(mealName);
                    alert(New Recipe Discovered: ${mealName});
                }
                updateInventory();
            } else {
                alert("You need more fish to cook!");
            }
        }

        function sellFood() {
            let earnings = mealInventory.length * 10 + cropInventory.length * 5;
            coins += earnings;
            mealInventory = [];
            cropInventory = [];
            updateInventory();
        }

        function buyItem(item) {
            if (item === "Rod" && coins >= 20) {
                coins -= 20;
                fishingLevel++;
                alert("Fishing gear upgraded!");
            } else if (item === "Bait" && coins >= 5) {
                coins -= 5;
                alert("Bait purchased!");
            } else if (item === "Seeds" && coins >= 3) {
                coins -= 3;
                cropInventory.push({ name: "Planted Crop" });
            } else {
                alert("Not enough coins!");
            }
            updateInventory();
        }

        function plantCrop() {
            setTimeout(() => {
                cropInventory.push({ name: "Harvested Crop" });
                updateInventory();
            }, 3000);
        }

        function harvestCrops() {
            if (cropInventory.length > 0) {
                alert("Crops harvested!");
                updateInventory();
            } else {
                alert("No crops to harvest!");
            }
        }

        function openStore() {
            document.querySelector(".store").classList.remove("hidden");
        }

        function closeStore() {
            document.querySelector(".store").classList.add("hidden");
        }

        function openFishTank() {
            document.querySelector(".fish-tank").classList.remove("hidden");
            document.getElementById("fishTankList").innerHTML = fishInventory.map(f => <li>${f.name} (${f.rarity})</li>).join('');
        }

        function closeFishTank() {
            document.querySelector(".fish-tank").classList.add("hidden");
        }

        function updateInventory() {
            document.getElementById('coins').textContent = coins;
            document.getElementById('fishingLevel').textContent = fishingLevel;
            document.getElementById('inventoryList').innerHTML = fishInventory.map(f => <li>${f.name} (${f.rarity})</li>).join('');
        }
    </script>
</body>
</html>
<!DOCTYPE


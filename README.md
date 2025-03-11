<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weed Empire Tycoon</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #2e2e2e;
            color: white;
        }
        .game-container {
            margin-top: 20px;
        }
        .button {
            font-size: 18px;
            padding: 10px;
            margin: 5px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            background-color: #4CAF50;
            color: white;
            transition: transform 0.2s, background-color 0.3s;
        }
        .button:hover {
            transform: scale(1.1);
        }
        .inventory, .store, .achievements {
            margin-top: 20px;
            padding: 10px;
            border: 2px solid white;
            background: #333;
            width: 300px;
            text-align: left;
            display: inline-block;
        }
        .inventory h3, .store h3, .achievements h3 {
            text-align: center;
        }
        .weed-detail {
            margin: 5px 0;
        }
        .weather, .location {
            font-size: 20px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>🌿 Weed Empire Tycoon 🌿</h1>
    <p>Grow, breed, sell, and create the ultimate cannabis empire!</p>

    <div class="game-container">
        <button class="button" onclick="growWeed()">🌱 Grow Weed</button>
        <button class="button" onclick="breedStrains()">💨 Breed Strains</button>
        <button class="button" onclick="makeEdible()">🍪 Make Edibles</button>
        <button class="button" onclick="makeJoint()">🚬 Make Joints</button>
        <button class="button" onclick="sellProducts()">💰 Sell Products</button>
        <button class="button" onclick="buyMoreLand()">🏡 Buy More Land</button>
        <button class="button" onclick="travel()">✈️ Travel for Rare Strains</button>
        <button class="button" onclick="visitStore()">🛒 Visit Store</button>
    </div>

    <div class="inventory">
        <h3>Inventory</h3>
        <p>Coins: 💰 <span id="coins">100</span></p>
        <p>Land: 🌾 <span id="land">1</span> plots</p>
        <p>Weed Weight: 🌿 <span id="weedWeight">0</span> grams</p>
        <ul id="weedList"></ul>
        <p>Products: 🍪 <span id="edibles">0</span>, 🚬 <span id="joints">0</span></p>
    </div>

    <div class="store" id="store" style="display: none;">
        <h3>Store</h3>
        <button class="button" onclick="buyUpgrade()">🛠 Upgrade Grow Gear (50💰)</button>
        <button class="button" onclick="buySeeds()">🌱 Buy Better Seeds (30💰)</button>
        <button class="button" onclick="closeStore()">❌ Close Store</button>
    </div>

    <div class="location">
        <h3>Location: <span id="location">Home Compound</span></h3>
        <p id="weather"></p>
    </div>

    <div class="achievements" id="achievements">
        <h3>Achievements</h3>
        <ul id="achievementsList"></ul>
    </div>

    <script>
        let coins = 100;
        let land = 1;
        let weedInventory = [];
        let ediblesCount = 0;
        let jointsCount = 0;
        let compoundName = "Home Compound";
        let weather = "Clear skies";
        let achievements = [];
        
        const strains = [
            {name: "OG Kush", thc: 20, rarity: "Common", origin: "USA", price: 50},
            {name: "Purple Haze", thc: 22, rarity: "Uncommon", origin: "Netherlands", price: 60},
            {name: "Blue Dream", thc: 25, rarity: "Rare", origin: "California", price: 70},
            {name: "Sour Diesel", thc: 30, rarity: "Epic", origin: "USA", price: 80},
            {name: "Pineapple Express", thc: 28, rarity: "Legendary", origin: "Hawaii", price: 90}
        ];

        function updateUI() {
            document.getElementById("coins").textContent = coins;
            document.getElementById("land").textContent = land;
            document.getElementById("weedWeight").textContent = weedInventory.reduce((acc, weed) => acc + weed.weight, 0);
            document.getElementById("edibles").textContent = ediblesCount;
            document.getElementById("joints").textContent = jointsCount;
            document.getElementById("weedList").innerHTML = weedInventory.map(weed => `<li>${weed.name} - ${weed.weight}g - ${weed.thc}% THC</li>`).join('');
            document.getElementById("achievementsList").innerHTML = achievements.map(ach => `<li>${ach}</li>`).join('');
            document.getElementById("weather").textContent = weather;
        }

        function growWeed() {
            if (weedInventory.length < land * 5) {
                let strain = strains[Math.floor(Math.random() * strains.length)];
                let weight = Math.floor(Math.random() * (5 - 2 + 1)) + 2;  // Random weight between 2 and 5 grams
                weedInventory.push({...strain, weight: weight});
                alert(`You grew some ${strain.name} weighing ${weight}g!`);
                checkAchievement("Grew 1 weed strain");
            } else {
                alert("Not enough space! Buy more land.");
            }
            updateUI();
        }

        function breedStrains() {
            if (weedInventory.length >= 2) {
                let strain = {name: "Hybrid-" + Math.random().toString(36).substring(7), thc: Math.floor(Math.random() * (40 - 15 + 1)) + 15, rarity: "Rare", origin: "Custom", price: 100, weight: 5};
                weedInventory.push(strain);
                alert(`You bred a new strain: ${strain.name}!`);
                checkAchievement("Bred a new strain");
            } else {
                alert("You need at least 2 strains to breed.");
            }
            updateUI();
        }

        function makeEdible() {
            if (weedInventory.length > 0) {
                let weed = weedInventory.pop();
                ediblesCount++;
                alert(`You made an edible with ${weed.name} containing ${weed.thc}% THC.`);
                updateUI();
            } else {
                alert("You need weed to make products!");
            }
        }

        function makeJoint() {
            if (weedInventory.length > 0) {
                let weed = weedInventory.pop();
                jointsCount++;
                alert(`You rolled a joint with ${weed.name} containing ${weed.thc}% THC.`);
                updateUI();
            } else {
                alert("You need weed to make products!");
            }
        }

        function sellProducts() {
            let earnings = (ediblesCount * 50) + (jointsCount * 40);
            coins += earnings;
            ediblesCount = 0;
            jointsCount = 0;
            alert(`You sold all your products for ${earnings}💰!`);
            updateUI();
        }

        function buyMoreLand() {
            if (coins >= 100) {
                coins -= 100;
                land++;
                alert("You bought more land!");
                updateUI();
            } else {
                alert("Not enough coins!");
            }
        }

        function travel() {
            let locations = ["California", "Hawaii", "Netherlands", "USA"];
            let newLocation = locations[Math.floor(Math.random() * locations.length)];
            weather = ["Clear skies", "Rain", "Thunderstorm", "Sunny"][Math.floor(Math.random() * 4)];
            document.getElementById("location").textContent = newLocation;
            updateUI();
        }

        function visitStore() {
            document.getElementById("store").style.display = "block";
        }

        function closeStore() {
            document.getElementById("store").style.display = "none";
        }

        function buyUpgrade() {
            if (coins >= 50) {
                coins -= 50;
                alert("You upgraded your grow gear!");
                updateUI();
            } else {
                alert("Not enough coins!");
            }
        }

        function buySeeds() {
            if (coins >= 30) {
                coins -= 30;
                alert("You bought better seeds!");
                updateUI();
            } else {
                alert("Not enough coins!");
            }
        }

        function checkAchievement(achievement) {
            if (!achievements.includes(achievement)) {
                achievements.push(achievement);
            }
            updateUI();
        }

        function setCompoundName() {
            compoundName = prompt("Enter a name for your compound:");
            alert(`Your compound is now named "${compoundName}".`);
            updateUI();
        }

        window.onload = () => {
            setCompoundName();
            updateUI();
        };

    </script>
</body>
</html>

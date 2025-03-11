<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weed Empire Tycoon</title>
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
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
        .inventory, .store {
            margin-top: 20px;
            padding: 10px;
            border: 2px solid white;
            background: #333;
            width: 300px;
            text-align: left;
            display: inline-block;
        }
        .inventory h3, .store h3 {
            text-align: center;
        }
    </style>
</head>
<body>

    <h1>🌿 Weed Empire Tycoon 🌿</h1>
    <p>Grow, breed, sell, and create the ultimate cannabis empire!</p>

    <div class="game-container">
        <button class="button" onclick="growWeed()">🌱 Grow Weed</button>
        <button class="button" onclick="breedStrains()">💨 Breed Strains</button>
        <button class="button" onclick="makeProduct()">🍪 Make Edibles/Joints</button>
        <button class="button" onclick="sellWeed()">💰 Sell Products</button>
        <button class="button" onclick="buyMoreLand()">🏡 Buy More Land</button>
        <button class="button" onclick="travel()">✈️ Travel for Rare Strains</button>
        <button class="button" onclick="visitStore()">🛒 Visit Store</button>
    </div>

    <div class="inventory">
        <h3>Inventory</h3>
        <p>Coins: 💰 <span id="coins">100</span></p>
        <p>Land: 🌾 <span id="land">1</span> plots</p>
        <p>Weed Strains: 🌿 <span id="weedCount">0</span></p>
        <ul id="weedList"></ul>
        <p>Products: 🍪 <span id="products">0</span></p>
    </div>

    <div class="store" id="store" style="display: none;">
        <h3>Store</h3>
        <button class="button" onclick="buyUpgrade()">🛠 Upgrade Grow Gear (50💰)</button>
        <button class="button" onclick="buySeeds()">🌱 Buy Better Seeds (30💰)</button>
        <button class="button" onclick="closeStore()">❌ Close Store</button>
    </div>

    <script>
        let coins = 100;
        let land = 1;
        let weedInventory = [];
        let productCount = 0;

        const strains = [
            "OG Kush", "Purple Haze", "Blue Dream", "Sour Diesel", "Pineapple Express",
            "White Widow", "Gorilla Glue", "Granddaddy Purple", "Gelato", "AK-47"
        ];

        function updateUI() {
            document.getElementById("coins").textContent = coins;
            document.getElementById("land").textContent = land;
            document.getElementById("weedCount").textContent = weedInventory.length;
            document.getElementById("products").textContent = productCount;
            document.getElementById("weedList").innerHTML = weedInventory.map(strain => `<li>${strain}</li>`).join('');
        }

        function growWeed() {
            if (weedInventory.length < land * 5) {
                let newStrain = strains[Math.floor(Math.random() * strains.length)];
                weedInventory.push(newStrain);
                alert(`You grew some ${newStrain}!`);
            } else {
                alert("Not enough space! Buy more land.");
            }
            updateUI();
        }

        function breedStrains() {
            if (weedInventory.length >= 2) {
                let newStrain = `Hybrid-${Math.random().toString(36).substring(7)}`;
                weedInventory.push(newStrain);
                alert(`You bred a new strain: ${newStrain}!`);
            } else {
                alert("You need at least 2 strains to breed.");
            }
            updateUI();
        }

        function makeProduct() {
            if (weedInventory.length > 0) {
                weedInventory.pop();
                productCount++;
                alert("You created an edible or joint!");
            } else {
                alert("You need weed to make products!");
            }
            updateUI();
        }

        function sellWeed() {
            let earnings = productCount * 20;
            coins += earnings;
            productCount = 0;
            alert(`You sold all your products for ${earnings}💰!`);
            updateUI();
        }

        function buyMoreLand() {
            if (coins >= 100) {
                coins -= 100;
                land++;
                alert("You bought more land!");
            } else {
                alert("Not enough coins!");
            }
            updateUI(); // This was missing the closing bracket earlier
        }

        function travel() {
            // Add your travel function here
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
                alert("Upgraded grow gear!");
                updateUI();
            } else {
                alert("Not enough coins!");
            }
        }

        function buySeeds() {
            if (coins >= 30) {
                coins -= 30;
                alert("Bought better seeds!");
                updateUI();
            } else {
                alert("Not enough coins!");
            }
        }
    </script>
</body>
</html>

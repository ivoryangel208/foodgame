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
            transition: background 1s;
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
            padding: 15px;
            border: 3px solid gold;
            background: linear-gradient(to right, #6441A5, #2a0845);
            width: 350px;
            text-align: left;
            display: none;
            color: #fff;
        }
        .store h3 {
            text-align: center;
            font-size: 22px;
            font-weight: bold;
            text-shadow: 2px 2px 4px gold;
        }
        .location {
            position: fixed;
            top: 20px;
            right: 20px;
            font-size: 20px;
            font-weight: bold;
            background: rgba(0, 0, 0, 0.5);
            padding: 10px;
            border-radius: 10px;
        }
        .compound-name {
            font-size: 24px;
            font-weight: bold;
            margin-top: 10px;
        }
    </style>
</head>
<body>

    <h1>🌿 Weed Empire Tycoon 🌿</h1>
    <p>Grow, breed, sell, and build your cannabis empire!</p>
    <div class="compound-name">Compound: <span id="compoundName">Unnamed</span></div>
    
    <div class="game-container">
        <button class="button" onclick="setCompoundName()">🏡 Name Your Compound</button>
        <button class="button" onclick="growWeed()">🌱 Grow Weed</button>
        <button class="button" onclick="breedStrains()">💨 Breed Strains</button>
        <button class="button" onclick="makeEdible()">🍪 Make Edibles</button>
        <button class="button" onclick="makeJoint()">🚬 Make Joints</button>
        <button class="button" onclick="sellWeed()">💰 Sell Products</button>
        <button class="button" onclick="buyMoreLand()">🏡 Buy More Land</button>
        <button class="button" onclick="travel()">✈️ Travel</button>
        <button class="button" onclick="toggleInventory()">📦 Inventory</button>
        <button class="button" onclick="toggleStore()">🛒 Visit Store</button>
    </div>

    <div class="inventory">
        <h3>Inventory</h3>
        <p>💰 Coins: <span id="coins">100</span></p>
        <p>🌾 Land: <span id="land">1</span> plots</p>
        <h4>🌿 Weed Inventory:</h4>
        <ul id="weedList"></ul>
        <h4>🍪 Products:</h4>
        <p>Edibles: <span id="edibles">0</span></p>
        <p>Joints: <span id="joints">0</span></p>
    </div>

    <div class="store">
        <h3>🌟 Luxury Store 🌟</h3>
        <button class="button" onclick="buyUpgrade()">🛠 Upgrade Gear (50💰)</button>
        <button class="button" onclick="buySeeds()">🌱 Buy Premium Seeds (30💰)</button>
        <button class="button" onclick="toggleStore()">❌ Close</button>
    </div>

    <div class="location" id="locationName">📍 Home</div>

    <script>
        let coins = localStorage.getItem("coins") ? parseInt(localStorage.getItem("coins")) : 100;
        let land = localStorage.getItem("land") ? parseInt(localStorage.getItem("land")) : 1;
        let weedInventory = JSON.parse(localStorage.getItem("weedInventory")) || [];
        let edibles = localStorage.getItem("edibles") ? parseInt(localStorage.getItem("edibles")) : 0;
        let joints = localStorage.getItem("joints") ? parseInt(localStorage.getItem("joints")) : 0;
        let compoundName = localStorage.getItem("compoundName") || "Unnamed";

        document.getElementById("compoundName").textContent = compoundName;

        function updateUI() {
            document.getElementById("coins").textContent = coins;
            document.getElementById("land").textContent = land;
            document.getElementById("weedList").innerHTML = weedInventory.map(strain => `<li>${strain}</li>`).join('');
            document.getElementById("edibles").textContent = edibles;
            document.getElementById("joints").textContent = joints;
            saveGame();
        }

        function saveGame() {
            localStorage.setItem("coins", coins);
            localStorage.setItem("land", land);
            localStorage.setItem("weedInventory", JSON.stringify(weedInventory));
            localStorage.setItem("edibles", edibles);
            localStorage.setItem("joints", joints);
            localStorage.setItem("compoundName", compoundName);
        }

        function setCompoundName() {
            let newName = prompt("Enter your compound's name:");
            if (newName) {
                compoundName = newName;
                document.getElementById("compoundName").textContent = newName;
                saveGame();
            }
        }

        function toggleInventory() {
            let inventory = document.querySelector(".inventory");
            inventory.style.display = (inventory.style.display === "none") ? "block" : "none";
        }

        function toggleStore() {
            let store = document.querySelector(".store");
            store.style.display = (store.style.display === "none") ? "block" : "none";
        }

        function growWeed() {
            if (weedInventory.length < land * 5) {
                let newStrain = "Strain-" + Math.random().toString(36).substring(7);
                weedInventory.push(newStrain);
                alert(`You grew ${newStrain}!`);
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

        function makeEdible() {
            if (weedInventory.length > 0) {
                weedInventory.pop();
                edibles++;
                alert("You made an edible!");
            } else {
                alert("No weed to make an edible.");
            }
            updateUI();
        }

        function makeJoint() {
            if (weedInventory.length > 0) {
                weedInventory.pop();
                joints++;
                alert("You rolled a joint!");
            } else {
                alert("No weed to make a joint.");
            }
            updateUI();
        }

        function travel() {
            let locations = ["California", "Jamaica", "Amsterdam", "Canada"];
            let newLocation = locations[Math.floor(Math.random() * locations.length)];
            document.getElementById("locationName").textContent = `📍 ${newLocation}`;
            document.body.style.background = ["green", "blue", "purple", "black"][Math.floor(Math.random() * 4)];
        }

        updateUI();
    </script>
</body>
</html>

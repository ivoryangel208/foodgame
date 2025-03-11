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
            transition: background 1s ease-in-out;
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
        .button:active {
            transform: scale(0.9);
        }
        .inventory, .store {
            margin-top: 20px;
            padding: 15px;
            border: 3px solid gold;
            background: linear-gradient(to right, #6441A5, #2a0845);
            width: 350px;
            text-align: left;
            color: white;
            opacity: 0;
            transform: translateY(-20px);
            transition: opacity 0.5s ease-out, transform 0.5s ease-out;
            display: none;
        }
        .show {
            opacity: 1;
            transform: translateY(0);
            display: block;
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
            opacity: 0;
            transform: translateX(50px);
            transition: opacity 1s ease-out, transform 1s ease-out;
        }
        .show-location {
            opacity: 1;
            transform: translateX(0);
        }
        .grow-weed {
            animation: fadeIn 0.5s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.9); }
            to { opacity: 1; transform: scale(1); }
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
        let coins = 100, land = 1, weedInventory = [], edibles = 0, joints = 0, compoundName = "Unnamed";

        function updateUI() {
            document.getElementById("coins").textContent = coins;
            document.getElementById("land").textContent = land;
            document.getElementById("weedList").innerHTML = weedInventory.map(strain => `<li class="grow-weed">${strain}</li>`).join('');
            document.getElementById("edibles").textContent = edibles;
            document.getElementById("joints").textContent = joints;
        }

        function setCompoundName() {
            let newName = prompt("Enter your compound's name:");
            if (newName) {
                compoundName = newName;
                document.getElementById("compoundName").textContent = newName;
            }
        }

        function toggleInventory() {
            let inventory = document.querySelector(".inventory");
            inventory.classList.toggle("show");
        }

        function toggleStore() {
            let store = document.querySelector(".store");
            store.classList.toggle("show");
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
            document.getElementById("locationName").classList.add("show-location");

            let colors = ["green", "blue", "purple", "black"];
            document.body.style.background = colors[Math.floor(Math.random() * colors.length)];
        }

        updateUI();
    </script>
</body>
</html>

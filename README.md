<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weed Game</title>
    <style>
        /* Store Popup Style */
        #storePopup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            border: 2px solid black;
            padding: 20px;
            width: 300px;
            text-align: center;
        }
        #storePopup h3 {
            margin-bottom: 20px;
        }
        .store-item {
            margin: 10px 0;
        }
    </style>
</head>
<body>

    <div id="game">
        <p id="money">Money: $0</p>
        <button id="growBtn">Grow Weed</button>
        <button id="craftJointBtn">Craft Joint</button>
        <button id="craftEdibleBtn">Craft Edible</button>
        <button id="sellBtn">Sell Product</button>
        
        <h3>Inventory:</h3>
        <ul id="inventory">
            <li>Weed: 0g</li>
            <li>Joints: 0</li>
            <li>Edibles: 0</li>
        </ul>

        <!-- Store Button -->
        <button id="storeBtn">Visit Store</button>

        <!-- Store Popup -->
        <div id="storePopup">
            <h3>Store</h3>
            <div class="store-item">
                <p>Seeds - $10</p>
                <button id="buySeeds">Buy Seeds</button>
            </div>
            <div class="store-item">
                <p>Grow Lights - $20</p>
                <button id="buyLights">Buy Grow Lights</button>
            </div>
            <div class="store-item">
                <p>Fertilizer - $30</p>
                <button id="buyFertilizer">Buy Fertilizer</button>
            </div>
            <button id="closeStore">Close Store</button>
        </div>
    </div>

    <script>
        // Initialize variables
        let money = 0;
        let weed = 0;
        let joints = 0;
        let edibles = 0;
        let seeds = 0; // Track how many seeds the player has
        let growLights = 0; // Track how many grow lights the player has
        let fertilizer = 0; // Track how many fertilizers the player has

        // Function to update the display
        function updateDisplay() {
            document.getElementById("money").textContent = `Money: $${money}`;
            document.getElementById("inventory").innerHTML = `
                <li>Weed: ${weed}g</li>
                <li>Joints: ${joints}</li>
                <li>Edibles: ${edibles}</li>
                <li>Seeds: ${seeds}</li>
                <li>Grow Lights: ${growLights}</li>
                <li>Fertilizer: ${fertilizer}</li>
            `;
        }

        // Function to grow weed
        function growWeed() {
            let amountGrown = Math.floor(Math.random() * 6) + 1; // Default growth 1-6g
            if (growLights > 0) {
                amountGrown *= 2; // Double the amount if grow lights are available
            }
            if (fertilizer > 0) {
                amountGrown += 2; // Add extra weed with fertilizer
            }
            if (seeds > 0) {
                seeds--; // Use 1 seed each time
                weed += amountGrown;
                updateDisplay();
            } else {
                alert("No seeds to grow!");
            }
        }

        // Function to craft a joint
        function craftJoint() {
            if (weed >= 1) {
                weed -= 1; // Deduct 1g of weed per joint
                joints += 1; // Add 1 joint
                updateDisplay();
            } else {
                alert("Not enough weed to craft a joint!");
            }
        }

        // Function to craft an edible
        function craftEdible() {
            if (weed >= 1) {
                weed -= 1; // Deduct 1g of weed per edible
                edibles += 1; // Add 1 edible
                updateDisplay();
            } else {
                alert("Not enough weed to craft an edible!");
            }
        }

        // Function to sell product
        function sellProduct() {
            let earnings = 0;
            if (joints > 0) {
                earnings += joints * 10; // Each joint sells for $10
                joints = 0; // Clear the joint inventory
            }
            if (edibles > 0) {
                earnings += edibles * 15; // Each edible sells for $15
                edibles = 0; // Clear the edible inventory
            }
            money += earnings;
            alert(`You sold products and earned $${earnings}!`);
            updateDisplay();
        }

        // Function to open store
        function openStore() {
            document.getElementById("storePopup").style.display = 'block'; // Show store
        }

        // Function to close store
        function closeStore() {
            document.getElementById("storePopup").style.display = 'none'; // Hide store
        }

        // Buying items from the store
        function buySeeds() {
            if (money >= 10) {
                money -= 10; // Deduct money for seeds
                seeds += 1; // Add 1 seed
                updateDisplay();
            } else {
                alert("Not enough money to buy seeds!");
            }
        }

        function buyLights() {
            if (money >= 20) {
                money -= 20; // Deduct money for grow lights
                growLights += 1; // Add 1 grow light
                updateDisplay();
            } else {
                alert("Not enough money to buy grow lights!");
            }
        }

        function buyFertilizer() {
            if (money >= 30) {
                money -= 30; // Deduct money for fertilizer
                fertilizer += 1; // Add 1 fertilizer
                updateDisplay();
            } else {
                alert("Not enough money to buy fertilizer!");
            }
        }

        // Event listeners for buttons
        document.getElementById("growBtn").addEventListener("click", growWeed);
        document.getElementById("craftJointBtn").addEventListener("click", craftJoint);
        document.getElementById("craftEdibleBtn").addEventListener("click", craftEdible);
        document.getElementById("sellBtn").addEventListener("click", sellProduct);

        // Store button interactions
        document.getElementById("storeBtn").addEventListener("click", openStore);
        document.getElementById("closeStore").addEventListener("click", closeStore);
        document.getElementById("buySeeds").addEventListener("click", buySeeds);
        document.getElementById("buyLights").addEventListener("click", buyLights);
        document.getElementById("buyFertilizer").addEventListener("click", buyFertilizer);

        // Initialize display
        updateDisplay();
    </script>

</body>
</html>

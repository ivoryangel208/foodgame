<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weed Farm Tycoon</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            color: #333;
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            text-align: center;
        }
        .button {
            padding: 10px 20px;
            margin: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 16px;
            border-radius: 5px;
        }
        .button:hover {
            background-color: #45a049;
        }
        .button:active {
            background-color: #3e8e41;
        }
        .inventory, .store, .grow-logs {
            margin-top: 20px;
            text-align: left;
        }
        .inventory ul, .store ul {
            list-style-type: none;
            padding: 0;
        }
        .inventory li, .store li {
            padding: 5px;
            margin-bottom: 5px;
            background-color: #e0e0e0;
            border-radius: 5px;
        }
        .grow-log {
            padding: 5px;
            margin-top: 5px;
            background-color: #f9f9f9;
            border-radius: 5px;
        }
        .emoji {
            font-size: 30px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Weed Farm Tycoon</h1>
        <p id="game-status">Welcome to your weed farm!</p>

        <div>
            <button id="grow-button" class="button">Grow Weed 🌱</button>
            <button id="harvest-button" class="button" disabled>Harvest Weed 🌾</button>
            <button id="make-joint-button" class="button" disabled>Make Joint 🌿</button>
            <button id="make-edible-button" class="button" disabled>Make Edible 🍪</button>
            <button id="make-dab-button" class="button" disabled>Make Dab 💨</button>
            <button id="sell-button" class="button" disabled>Sell Weed 💸</button>
            <button id="travel-button" class="button">Travel 🗺️</button>
        </div>

        <div class="inventory">
            <h3>Your Inventory:</h3>
            <div><strong>Money: </strong><span id="money-count">100</span></div>
            <h4>Plants</h4>
            <ul id="plant-list">
                <li>No plants yet!</li>
            </ul>
            <h4>Processed Products</h4>
            <ul id="processed-list">
                <li>No products made yet!</li>
            </ul>
        </div>

        <div class="store">
            <h3>Store:</h3>
            <ul id="store-list">
                <li>Buy Strain Seeds 🌱</li>
                <li>Buy Mystery Box 🎁</li>
            </ul>
        </div>

        <div class="grow-logs">
            <h3>Grow Logs:</h3>
            <ul id="grow-log-list">
                <li>No logs yet!</li>
            </ul>
        </div>
    </div>

    <script>
        // Game Variables
        let plants = [];
        let money = 100;
        let plantCount = 0;
        let isPlantReady = false;

        // Processed products
        let processedProducts = {
            joints: 0,
            edibles: 0,
            dabs: 0
        };

        // Strain Data
        const strains = [
            { name: "Blue Dream", thc: "20%", country: "USA", rarity: "Common", price: 50 },
            { name: "OG Kush", thc: "24%", country: "USA", rarity: "Rare", price: 70 },
            { name: "Northern Lights", thc: "22%", country: "Afghanistan", rarity: "Legendary", price: 100 },
            { name: "Gelato", thc: "26%", country: "Italy", rarity: "Epic", price: 120 }
        ];

        // Update the UI
        function updateUI() {
            // Update status
            document.getElementById("game-status").textContent = `Money: $${money}`;

            // Update Money
            document.getElementById("money-count").textContent = money;

            // Update Plant Inventory
            const plantList = document.getElementById("plant-list");
            plantList.innerHTML = "";
            if (plants.length === 0) {
                plantList.innerHTML = "<li>No plants yet!</li>";
            } else {
                plants.forEach((plant, index) => {
                    const plantItem = document.createElement("li");
                    plantItem.textContent = `${plant.name} (${plant.thc} THC) - Status: ${plant.status} - Time Left: ${plant.timeLeft} day(s)`;
                    plantList.appendChild(plantItem);
                });
            }

            // Update Processed Products
            const processedList = document.getElementById("processed-list");
            processedList.innerHTML = "";
            if (processedProducts.joints > 0) {
                processedList.innerHTML += `<li>Joints: ${processedProducts.joints}</li>`;
            }
            if (processedProducts.edibles > 0) {
                processedList.innerHTML += `<li>Edibles: ${processedProducts.edibles}</li>`;
            }
            if (processedProducts.dabs > 0) {
                processedList.innerHTML += `<li>Dabs: ${processedProducts.dabs}</li>`;
            }
            if (processedList.innerHTML === "") {
                processedList.innerHTML = "<li>No products made yet!</li>";
            }

            // Update Grow Logs
            const growLogList = document.getElementById("grow-log-list");
            growLogList.innerHTML = "";
            plants.forEach((plant, index) => {
                if (plant.status === "Growing") {
                    const logItem = document.createElement("li");
                    logItem.textContent = `Growing ${plant.name}... (Harvest in ${plant.timeLeft} days)`;
                    growLogList.appendChild(logItem);
                }
            });
        }

        // Grow a Plant
        document.getElementById("grow-button").addEventListener("click", () => {
            if (plantCount < 5) {
                const strain = strains[Math.floor(Math.random() * strains.length)];
                const newPlant = {
                    name: strain.name,
                    thc: strain.thc,
                    country: strain.country,
                    rarity: strain.rarity,
                    price: strain.price,
                    status: "Growing",
                    timeLeft: Math.floor(Math.random() * 6) + 1 // Time between 1 and 6 days
                };
                plants.push(newPlant);
                plantCount++;
                updateUI();
                document.getElementById("harvest-button").disabled = false;
                document.getElementById("make-joint-button").disabled = false;
                document.getElementById("make-edible-button").disabled = false;
                document.getElementById("make-dab-button").disabled = false;
            } else {
                alert("You can only grow 5 plants at once!");
            }
        });

        // Harvest Plant
        document.getElementById("harvest-button").addEventListener("click", () => {
            if (plants.length > 0) {
                const plant = plants[plants.length - 1];
                if (plant.status === "Growing" && plant.timeLeft === 1) {
                    plant.status = "Ready to Harvest";
                    alert(`${plant.name} is ready to harvest!`);
                } else {
                    alert(`${plant.name} is not ready yet!`);
                }
            }
            updateUI();
        });

        // Make Joint, Edible, Dab
        document.getElementById("make-joint-button").addEventListener("click", () => {
            const plant = plants[plants.length - 1];
            if (plant.status === "Ready to Harvest") {
                money += 10;
                processedProducts.joints++;
                alert(`Made a joint from ${plant.name}.`);
                plants.pop();
                updateUI();
            }
        });

        document.getElementById("make-edible-button").addEventListener("click", () => {
            const plant = plants[plants.length - 1];
            if (plant.status === "Ready to Harvest") {
                money += 15;
                processedProducts.edibles++;
                alert(`Made an edible from ${plant.name}.`);
                plants.pop();
                updateUI();
            }
        });

        document.getElementById("make-dab-button").addEventListener("click", () => {
            const plant = plants[plants.length - 1];
            if (plant.status === "Ready to Harvest") {
                money += 20;
                processedProducts.dabs++;
                alert(`Made a dab from ${plant.name}.`);
                plants.pop();
                updateUI();
            }
        });

        // Sell Products
        document.getElementById("sell-button").addEventListener("click", () => {
            if (processedProducts.joints > 0 || processedProducts.edibles > 0 || processedProducts.dabs > 0) {
                const revenue = processedProducts.joints * 10 + processedProducts.edibles * 15 + processedProducts.dabs * 20;
                money += revenue;
                processedProducts.joints = 0;
                processedProducts.edibles = 0;
                processedProducts.dabs = 0;
                updateUI();
                alert(`Sold all products for $${revenue}.`);
            } else {
                alert("No products to sell!");
            }
        });

        // Travel to the Store (Placeholder for store features)
        document.getElementById("travel-button").addEventListener("click", () => {
            alert("You traveled to the store!");
        });

        // Initial UI Update
        updateUI();
    </script>
</body>
</html>

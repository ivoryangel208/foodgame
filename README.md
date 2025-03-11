<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
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
        }
        .inventory, .index {
            margin-top: 20px;
            padding: 10px;
            border: 2px solid black;
            display: inline-block;
            background: white;
            font-size: 18px;
            text-align: left;
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
        <button class="button farm-btn" onclick="farmCrops(); changeBackground('#8BC34A')">🌾 Farm</button>
        <button class="button travel-btn" onclick="travel(); changeBackground('#FF5722')">🚗 Travel</button>
        <button class="button quest-btn" onclick="startQuest(); changeBackground('#795548')">🏡 Quest</button>
        <button class="button contest-btn" onclick="enterContest(); changeBackground('#FFC107')">🏆 Enter Cooking Contest</button>
    </div>

    <div class="inventory">
        <h3>Inventory</h3>
        <p>Fish: <span id="fishCount">0</span></p>
        <p>Meals: <span id="mealCount">0</span></p>
        <p>Coins: 💰 <span id="coins">0</span></p>
        <p>Fishing Level: 🎣 <span id="fishingLevel">1</span></p>
        <p>Crops: 🌾 <span id="cropCount">0</span></p>
        <p>Travel Location: <span id="locations">Home</span></p>
        <p id="fishDetails"> </p> <!-- Added for displaying details of fish caught -->
    </div>

    <div class="index">
        <h3>Game Index</h3>
        <p><strong>Tools:</strong> Basic Rod, Advanced Rod, Cooking Pot, Farming Tools</p>
        <p><strong>Meals:</strong> Grilled Fish, Fish Soup, Sushi, Fried Rice</p>
        <p><strong>Food:</strong> Fish, Crops, Spices</p>
        <p><strong>Cars:</strong> Bike, Old Truck, Speedboat</p>
        <p><strong>Upgrades:</strong> Better Fishing Gear, Farm Expansion, Cooking Equipment</p>
    </div>

    <script>
        // Randomized fish/animal attributes
        let speciesList = ['Bass', 'Trout', 'Salmon', 'Shark', 'Whale'];
        let rarityList = ['Common', 'Uncommon', 'Rare', 'Epic', 'Legendary'];
        let weightList = ['1kg', '2kg', '3kg', '500kg', '1000kg'];
        let lengthList = ['30cm', '50cm', '60cm', '4m', '15m'];
        let priceList = [5, 10, 15, 25, 100];
        let descriptionList = [
            'A common freshwater fish.',
            'A popular fish known for its delicious taste.',
            'A fish prized for its rich flavor and pink meat.',
            'A massive predator of the seas.',
            'The giant of the oceans.'
        ];
        let nicknamesList = ['Finn', 'Splash', 'Bubbles', 'Jaws', 'Whaley'];

        let fishCount = 0;
        let mealCount = 0;
        let coins = 0;
        let fishingLevel = 1;
        let cropCount = 0;
        let currentLocation = 0;

        function changeBackground(color) {
            document.body.style.backgroundColor = color;
        }

        function randomizeAttributes() {
            let species = speciesList[Math.floor(Math.random() * speciesList.length)];
            let rarity = rarityList[Math.floor(Math.random() * rarityList.length)];
            let weight = weightList[Math.floor(Math.random() * weightList.length)];
            let length = lengthList[Math.floor(Math.random() * lengthList.length)];
            let price = priceList[Math.floor(Math.random() * priceList.length)];
            let description = descriptionList[Math.floor(Math.random() * descriptionList.length)];
            let nickname = nicknamesList[Math.floor(Math.random() * nicknamesList.length)];

            return {
                species: species,
                rarity: rarity,
                weight: weight,
                length: length,
                price: price,
                description: description,
                nickname: nickname
            };
        }

        function goFishing() {
            let newFish = randomizeAttributes();
            fishCount += fishingLevel;
            document.getElementById('fishCount').textContent = fishCount;
            
            // Displaying the details of the fish caught
            document.getElementById('fishDetails').innerHTML = `
                <strong>Fish Caught:</strong> ${newFish.species} (${newFish.nickname})<br>
                <strong>Weight:</strong> ${newFish.weight}<br>
                <strong>Length:</strong> ${newFish.length}<br>
                <strong>Rarity:</strong> ${newFish.rarity}<br>
                <strong>Price:</strong> 💰${newFish.price}<br>
                <strong>Description:</strong> ${newFish.description}
            `;
        }

        function cookFood() {
            if (fishCount > 0) {
                mealCount++;
                fishCount--;
                document.getElementById('fishCount').textContent = fishCount;
                document.getElementById('mealCount').textContent = mealCount;
            } else {
                alert("You need more fish to cook!");
            }
        }

        function sellFood() {
            if (mealCount > 0) {
                coins += 5 * mealCount;
                mealCount = 0;
                document.getElementById('coins').textContent = coins;
                document.getElementById('mealCount').textContent = mealCount;
            } else {
                alert("You have no food to sell!");
            }
        }

        function buyUpgrade() {
            if (coins >= 20) {
                coins -= 20;
                fishingLevel++;
                document.getElementById('coins').textContent = coins;
                document.getElementById('fishingLevel').textContent = fishingLevel;
                alert("You upgraded your fishing gear! Catch more fish!");
            } else {
                alert("Not enough coins for an upgrade!");
            }
        }

        function farmCrops() {
            cropCount++;
            document.getElementById('cropCount').textContent = cropCount;
        }

        function travel() {
            currentLocation = (currentLocation + 1) % ['Home', 'River', 'Town', 'Forest'].length;
            document.getElementById('locations').textContent = ['Home', 'River', 'Town', 'Forest'][currentLocation];
            alert("You traveled to " + ['Home', 'River', 'Town', 'Forest'][currentLocation] + "!");
        }

        function startQuest() {
            alert("A villager asks you to bring them a rare fish! Complete the quest for rewards!");
        }

        function enterContest() {
            if (mealCount > 0) {
                let success = Math.random() > 0.5;
                if (success) {
                    coins += 50;
                    alert("You won the cooking contest! Prize: 50 coins!");
                } else {
                    alert("You lost the contest, better luck next time!");
                }
                document.getElementById('coins').textContent = coins;
            } else {
                alert("You need a meal to enter the contest!");
            }
        }
    </script>
</body>
</html>

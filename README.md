
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weed Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            color: #333;
            text-align: center;
        }
        #inventory, #store, #strainDetails, #gameInfo, #growArea, #upgrades {
            margin: 20px;
            padding: 10px;
            border: 2px solid #ccc;
            border-radius: 5px;
            background-color: white;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 20px;
            margin: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .inventory-item, .strain-item {
            margin: 5px 0;
        }
        .emoji {
            font-size: 20px;
        }
        .upgrade-item {
            margin: 10px;
        }
        #growArea {
            display: flex;
            justify-content: center;
        }
        #gameInfo {
            margin-top: 20px;
        }
    </style>
</head>
<body>

<h1>🌿 Welcome to the Weed Game! 🌿</h1>

<div id="gameInfo">
    <p>Your balance: <span id="balance">100</span> 💰</p>
    <p>Your farm level: <span id="farmLevel">1</span></p>
    <p>Owned Properties: <span id="properties">None</span></p>
</div>

<div id="growArea">
    <button onclick="growPlant()">Grow Weed 🌱</button>
    <button onclick="growBulk()">Grow Bulk (1 oz) 🌿</button>
</div>

<div id="inventory">
    <h2>Your Inventory 🛒</h2>
    <div id="weedInventory"></div>
    <div id="ediblesInventory"></div>
    <div id="jointsInventory"></div>
    <div id="waxInventory"></div>
</div>

<div id="store">
    <h2>Store 🏪</h2>
    <button onclick="buyUpgrade()">Upgrade Farm (+$50)</button>
    <button onclick="buyStrain()">Buy Strain ($100)</button>
    <button onclick="sellWeed()">Sell Weed 💸</button>
    <button onclick="sellBulkWeed()">Sell Bulk Weed 💸</button>
</div>

<div id="strainDetails">
    <h2>Strains 💨</h2>
    <div id="strainList"></div>
</div>

<script>
    let balance = 100;
    let farmLevel = 1;
    let properties = [];
    let weedInventory = 0; // In grams
    let ediblesInventory = 0;
    let jointsInventory = 0;
    let waxInventory = 0;
    let strains = [
        {name: "Blue Dream", THC: "20%", country: "USA", rarity: "Common", price: 100},
        {name: "OG Kush", THC: "25%", country: "USA", rarity: "Rare", price: 150},
        {name: "Purple Haze", THC: "22%", country: "Colombia", rarity: "Epic", price: 200},
    ];

    // Update Game Information
    function updateGameInfo() {
        document.getElementById('balance').textContent = balance;
        document.getElementById('farmLevel').textContent = farmLevel;
        document.getElementById('properties').textContent = properties.join(", ") || "None";
        document.getElementById('weedInventory').innerHTML = `Weed: ${weedInventory}g`;
        document.getElementById('ediblesInventory').innerHTML = `Edibles: ${ediblesInventory}`;
        document.getElementById('jointsInventory').innerHTML = `Joints: ${jointsInventory}`;
        document.getElementById('waxInventory').innerHTML = `Wax: ${waxInventory}`;
    }

    // Grow Weed in Bulk (Ounces)
    function growBulk() {
        let plantYield = 28; // 1 ounce = 28 grams
        weedInventory += plantYield;
        balance += 20; // Increase balance slightly for bulk growing
        updateGameInfo();
        alert(`You grew 1 ounce (28g) of weed!`);
    }

    // Grow a Single Plant (Random yield between 1 and 10 grams)
    function growPlant() {
        let plantYield = Math.floor(Math.random() * 10) + 1;
        weedInventory += plantYield;
        balance += 10; // Increase balance slightly after growing
        updateGameInfo();
        alert(`You grew ${plantYield}g of weed!`);
    }

    // Sell Weed (Bulk or Individual grams)
    function sellWeed() {
        if (weedInventory >= 1) {
            let weedToSell = Math.floor(Math.random() * weedInventory) + 1;
            weedInventory -= weedToSell;
            balance += weedToSell * 10;
            updateGameInfo();
            alert(`You sold ${weedToSell}g of weed for $${weedToSell * 10}`);
        } else {
            alert("You don't have enough weed to sell.");
        }
    }

    // Sell Bulk Weed (Ounces)
    function sellBulkWeed() {
        if (weedInventory >= 28) { // 1 ounce = 28 grams
            let bulkToSell = Math.floor(weedInventory / 28);
            let amountSold = bulkToSell * 28;
            weedInventory -= amountSold;
            balance += bulkToSell * 250; // Sell bulk weed for $250 per ounce
            updateGameInfo();
            alert(`You sold ${bulkToSell} ounces (${amountSold}g) of weed for $${bulkToSell * 250}`);
        } else {
            alert("You don't have enough weed to sell in bulk.");
        }
    }

    // Buy Strain
    function buyStrain() {
        if (balance >= 100) {
            balance -= 100;
            let strain = strains[Math.floor(Math.random() * strains.length)];
            properties.push(strain.name);
            alert(`You bought ${strain.name} strain!`);
            updateGameInfo();
        } else {
            alert("Not enough balance to buy strain.");
        }
    }

    // Make Joint (Bulk Option)
    function makeJoint() {
        let jointCount = Math.floor(weedInventory / 1); // Make a joint from 1g of weed
        if (weedInventory >= jointCount) {
            weedInventory -= jointCount;
            jointsInventory += jointCount;
            updateGameInfo();
            alert(`You made ${jointCount} joints!`);
        } else {
            alert("Not enough weed to make joints.");
        }
    }

    // Make Edible (Bulk Option)
    function makeEdible() {
        let edibleCount = Math.floor(weedInventory / 0.5); // Make an edible from 0.5g of weed
        if (weedInventory >= edibleCount * 0.5) {
            weedInventory -= edibleCount * 0.5;
            ediblesInventory += edibleCount;
            updateGameInfo();
            alert(`You made ${edibleCount} edibles!`);
        } else {
            alert("Not enough weed to make edibles.");
        }
    }

    // Make Wax (Bulk Option)
    function makeWax() {
        let waxCount = Math.floor(weedInventory / 2); // Make wax from 2g of weed
        if (weedInventory >= waxCount * 2) {
            weedInventory -= waxCount * 2;
            waxInventory += waxCount;
            updateGameInfo();
            alert(`You made ${waxCount} wax!`);
        } else {
            alert("Not enough weed to make wax.");
        }
    }

    // Display Strains
    function displayStrains() {
        let strainList = document.getElementById('strainList');
        strainList.innerHTML = '';
        strains.forEach(strain => {
            let strainElement = document.createElement('div');
            strainElement.classList.add('strain-item');
            strainElement.innerHTML = `${strain.name} - THC: ${strain.THC}, Country: ${strain.country}, Rarity: ${strain.rarity}, Price: $${strain.price}`;
            strainList.appendChild(strainElement);
        });
    }

    // Initial UI updates
    displayStrains();
    updateGameInfo();

    // Event Listeners for making products
    const makeJointButton = document.createElement("button");
    makeJointButton.textContent = "Make Joint 🚬";
    makeJointButton.onclick = makeJoint;
    document.getElementById('inventory').appendChild(makeJointButton);

    const makeEdibleButton = document.createElement("button");
    makeEdibleButton.textContent = "Make Edible 🍪";
    makeEdibleButton.onclick = makeEdible;
    document.getElementById('inventory').appendChild(makeEdibleButton);

    const makeWaxButton = document.createElement("button");
    makeWaxButton.textContent = "Make Wax 🧴";
    makeWaxButton.onclick = makeWax;
    document.getElementById('inventory').appendChild(makeWaxButton);

</script>

</body>
</html>

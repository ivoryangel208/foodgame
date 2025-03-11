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
        #inventory, #store, #strainDetails {
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
        #game-info {
            margin-top: 20px;
        }
        .emoji {
            font-size: 20px;
        }
    </style>
</head>
<body>

<h1>🌿 Welcome to the Weed Game! 🌿</h1>

<div id="game-info">
    <p>Your balance: <span id="balance">100</span> 💰</p>
    <p>Strain Level: <span id="strain-level">10%</span></p>
    <p>Owned Properties: <span id="properties">None</span></p>
</div>

<div id="inventory">
    <h2>Your Inventory 🛒</h2>
    <div id="weed-inventory">
        <!-- Weed inventory will be displayed here -->
    </div>
    <button onclick="addWeed()">Add Weed 🌱</button>
    <button onclick="consumeEdible()">Consume Edible 🍪</button>
    <button onclick="smokeJoint()">Smoke Joint 🚬</button>
</div>

<div id="store">
    <h2>Store 🏬</h2>
    <button onclick="buyStrain()">Buy Strain 🌿</button>
    <button onclick="buyEdible()">Buy Edible 🍩</button>
    <button onclick="buyJoint()">Buy Joint 🚬</button>
    <button onclick="buyProperty()">Buy Property 🏡</button>
</div>

<div id="strainDetails">
    <h2>Strain Details 🔍</h2>
    <p id="strain-info">Click on a strain to see details.</p>
</div>

<script>
// Game data
let inventory = [];
let balance = 100;
let ownedProperties = [];

// Strains available in the store
let strains = [
    { name: "Blue Dream", thc: 20, origin: "California", rarity: "Common", price: 10 },
    { name: "OG Kush", thc: 25, origin: "USA", rarity: "Rare", price: 15 },
    { name: "Granddaddy Purple", thc: 22, origin: "California", rarity: "Common", price: 12 },
    { name: "Girl Scout Cookies", thc: 18, origin: "USA", rarity: "Legendary", price: 20 }
];

// Edibles and joints
let edibles = [{ name: "Cannabis Brownie", thc: 50, price: 5 }];
let joints = [{ name: "Pre-Rolled Joint", thc: 100, price: 7 }];

// Update balance and display weed in inventory
function updateBalance(amount) {
    balance += amount;
    document.getElementById('balance').textContent = balance;
}

// Add weed to inventory
function addWeed() {
    let strain = strains[Math.floor(Math.random() * strains.length)];
    inventory.push({ strain: strain.name, thc: strain.thc });
    displayInventory();
}

// Consume an edible
function consumeEdible() {
    if (edibles.length > 0) {
        let edible = edibles[0];
        inventory.push({ strain: "Edible", thc: edible.thc });
        edibles.pop(); // Remove the edible after consumption
        displayInventory();
        alert("You consumed a " + edible.name + "!");
    } else {
        alert("No edibles in your inventory!");
    }
}

// Smoke a joint
function smokeJoint() {
    if (joints.length > 0) {
        let joint = joints[0];
        inventory.push({ strain: "Joint", thc: joint.thc });
        joints.pop(); // Remove the joint after use
        displayInventory();
        alert("You smoked a " + joint.name + "!");
    } else {
        alert("No joints in your inventory!");
    }
}

// Display inventory
function displayInventory() {
    let inventoryDiv = document.getElementById('weed-inventory');
    inventoryDiv.innerHTML = "";
    inventory.forEach(item => {
        let div = document.createElement('div');
        div.classList.add('inventory-item');
        div.textContent = item.strain + " (" + item.thc + "mg THC)";
        inventoryDiv.appendChild(div);
    });
}

// Buy a strain
function buyStrain() {
    let strain = strains[Math.floor(Math.random() * strains.length)];
    if (balance >= strain.price) {
        updateBalance(-strain.price);
        alert("You bought " + strain.name + " for " + strain.price + " coins.");
    } else {
        alert("You don't have enough coins!");
    }
}

// Buy an edible
function buyEdible() {
    if (balance >= edibles[0].price) {
        updateBalance(-edibles[0].price);
        alert("You bought a " + edibles[0].name);
    } else {
        alert("You don't have enough coins!");
    }
}

// Buy a joint
function buyJoint() {
    if (balance >= joints[0].price) {
        updateBalance(-joints[0].price);
        alert("You bought a " + joints[0].name);
    } else {
        alert("You don't have enough coins!");
    }
}

// Buy a property
function buyProperty() {
    let propertyName = prompt("Enter the name of your new property:");
    if (propertyName) {
        ownedProperties.push(propertyName);
        document.getElementById('properties').textContent = ownedProperties.join(", ");
        updateBalance(-50); // Deduct 50 coins for property purchase
    }
}

// Show strain details
function showStrainDetails(strain) {
    let strainInfo = `Name: ${strain.name}<br>THC Level: ${strain.thc}%<br>Origin: ${strain.origin}<br>Rarity: ${strain.rarity}<br>Price: ${strain.price} coins`;
    document.getElementById('strain-info').innerHTML = strainInfo;
}
</script>

</body>
</html>

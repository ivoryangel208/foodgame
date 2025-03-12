<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Farm-to-Table Cooking Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            text-align: center;
        }

        button {
            background-color: #4CAF50;
            color: white;
            font-size: 16px;
            padding: 10px 20px;
            border: none;
            cursor: pointer;
            margin: 10px;
        }

        button:hover {
            background-color: #45a049;
        }

        .dish-card {
            background-color: #fff;
            padding: 20px;
            margin: 10px;
            border-radius: 5px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            width: 300px;
            display: inline-block;
            vertical-align: top;
            text-align: left;
        }

        .inventory {
            margin-top: 30px;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
        }

        .dish-title {
            font-size: 18px;
            font-weight: bold;
        }

        .dish-description {
            font-size: 14px;
            margin-bottom: 10px;
        }

        .dish-rating {
            font-size: 16px;
            color: #f39c12;
        }

        .price {
            font-size: 16px;
            color: #e74c3c;
            margin-bottom: 10px;
        }

        .sell-button {
            background-color: #3498db;
        }

        .inventory-title {
            font-size: 24px;
            font-weight: bold;
            margin-top: 20px;
        }

        .total-money {
            font-size: 20px;
            font-weight: bold;
            color: #2ecc71;
            margin-top: 20px;
        }

        .ingredients-list {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .ingredient-button {
            background-color: #3498db;
        }
    </style>
</head>
<body>

<h1>🍽️ Farm-to-Table Cooking Game 🍽️</h1>

<!-- Select Dish Section -->
<div>
    <h2>🌱 Choose Ingredients</h2>
    <div class="ingredients-list">
        <button id="addMeatButton" class="ingredient-button">🐗 Add Exotic Meat</button>
        <button id="addFishButton" class="ingredient-button">🐟 Add Exotic Fish</button>
        <button id="addPlantButton" class="ingredient-button">🌿 Add Exotic Plant</button>
        <button id="createDishButton" class="ingredient-button">🍳 Create Dish</button>
    </div>
</div>

<!-- Dish Creation Section -->
<div id="dishCreationSection" style="display: none;">
    <h2>🍴 Create a Dish</h2>
    <input type="text" id="dishName" placeholder="Dish Name">
    <input type="number" id="dishPrice" placeholder="Price" step="0.01">
    <textarea id="dishDescription" placeholder="Describe your dish"></textarea>
    <input type="number" id="dishRating" placeholder="Rating (1-5)" max="5" min="1">
    <button id="saveDishButton" class="ingredient-button">💾 Save Dish</button>
</div>

<!-- Inventory Section -->
<div class="inventory-title">🍲 Your Dishes</div>
<div class="inventory" id="inventory"></div>

<!-- Sell Section -->
<div class="total-money">💵 Total Money: $<span id="totalMoney">0.00</span></div>

<script>
    let totalMoney = 0;
    let currentDish = { name: "", ingredients: [], description: "", price: 0, rating: 0 };
    let inventory = [];

    // Exotic Ingredients
    const ingredients = {
        meats: ["Kangaroo 🦘", "Bison 🐃", "Ostrich 🦢", "Alpaca 🦙", "Venison 🦌", "Wild Boar 🐗", "Camel 🐪", "Crocodile 🐊", "Emu 🦩", "Alligator 🐊"],
        fish: ["Tuna 🐟", "Swordfish 🗡️🐟", "Piranha 🐠", "Salmon 🐟", "Mahi Mahi 🐟", "Octopus 🐙", "Snapper 🐟", "Barracuda 🐟", "Tarpan 🐟", "Anglerfish 🐟"],
        plants: ["Edible Flowers 🌸", "Wild Herbs 🌿", "Ginger 🌱", "Saffron 🌺", "Kale 🥬", "Lavender 🌸", "Truffles 🍄", "Chili Peppers 🌶️", "Bamboo Shoots 🎋", "Mushrooms 🍄"]
    };

    // Event Listeners
    const addMeatButton = document.getElementById("addMeatButton");
    const addFishButton = document.getElementById("addFishButton");
    const addPlantButton = document.getElementById("addPlantButton");
    const createDishButton = document.getElementById("createDishButton");
    const saveDishButton = document.getElementById("saveDishButton");
    const inventoryDiv = document.getElementById("inventory");
    const totalMoneySpan = document.getElementById("totalMoney");
    const dishNameInput = document.getElementById("dishName");
    const dishPriceInput = document.getElementById("dishPrice");
    const dishDescriptionInput = document.getElementById("dishDescription");
    const dishRatingInput = document.getElementById("dishRating");

    // Functions for adding ingredients
    addMeatButton.addEventListener("click", () => {
        currentDish.ingredients.push(ingredients.meats[Math.floor(Math.random() * ingredients.meats.length)]);
        alert("🍖 Added an exotic meat to your dish!");
    });

    addFishButton.addEventListener("click", () => {
        currentDish.ingredients.push(ingredients.fish[Math.floor(Math.random() * ingredients.fish.length)]);
        alert("🐟 Added an exotic fish to your dish!");
    });

    addPlantButton.addEventListener("click", () => {
        currentDish.ingredients.push(ingredients.plants[Math.floor(Math.random() * ingredients.plants.length)]);
        alert("🌿 Added an exotic plant to your dish!");
    });

    // Create Dish Button - Show dish creation section
    createDishButton.addEventListener("click", () => {
        document.getElementById("dishCreationSection").style.display = "block";
    });

    // Save Dish Button - Save and add dish to inventory
    saveDishButton.addEventListener("click", () => {
        const name = dishNameInput.value;
        const price = parseFloat(dishPriceInput.value);
        const description = dishDescriptionInput.value;
        const rating = parseInt(dishRatingInput.value);

        if (name && price > 0 && description && rating >= 1 && rating <= 5) {
            inventory.push({
                name,
                ingredients: [...currentDish.ingredients],
                description,
                price,
                rating
            });

            currentDish = { name: "", ingredients: [], description: "", price: 0, rating: 0 };
            dishNameInput.value = "";
            dishPriceInput.value = "";
            dishDescriptionInput.value = "";
            dishRatingInput.value = "";

            // Re-render Inventory
            renderInventory();
        } else {
            alert("⚠️ Please fill in all fields correctly.");
        }

        // Hide dish creation section after saving
        document.getElementById("dishCreationSection").style.display = "none";
    });

    // Render Inventory
    function renderInventory() {
        inventoryDiv.innerHTML = "";
        inventory.forEach(dish => {
            const dishCard = document.createElement("div");
            dishCard.classList.add("dish-card");

            dishCard.innerHTML = `
                <div class="dish-title">${dish.name}</div>
                <div class="dish-description">${dish.description}</div>
                <div class="price">💸 $${dish.price.toFixed(2)}</div>
                <div class="dish-rating">⭐ Rating: ${dish.rating}/5</div>
                <button class="sell-button" onclick="sellDish(${inventory.indexOf(dish)})">🛒 Sell</button>
                <div class="ingredients">🥘 Ingredients: ${dish.ingredients.join(", ")}</div>
            `;
            inventoryDiv.appendChild(dishCard);
        });
    }

    // Sell Dish and Update Money
    function sellDish(dishIndex) {
        const dish = inventory[dishIndex];
        totalMoney += dish.price;
        totalMoneySpan.textContent = totalMoney.toFixed(2);
        inventory.splice(dishIndex, 1);
        renderInventory();
    }

</script>

</body>
</html>



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

        .ingredient-description {
            font-size: 12px;
            color: #555;
            margin-top: 5px;
        }

        .ingredient-list {
            text-align: left;
            margin-top: 20px;
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

<!-- Ingredient Descriptions -->
<div id="ingredientDescriptions" class="ingredient-list" style="display: none;">
    <h2>🍽️ Ingredient Descriptions</h2>
    <p id="ingredientText"></p>
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

    // Exotic Ingredients and Descriptions
    const ingredients = {
        meats: [
            { name: "Kangaroo 🦘", description: "A lean and tender meat, often cooked on the grill. Known for its unique flavor and rich protein content." },
            { name: "Bison 🐃", description: "A rich and flavorful red meat, lower in fat than beef, often used in gourmet dishes." },
            { name: "Ostrich 🦢", description: "An exotic, tender, and lean red meat, often compared to beef in flavor but much lighter." },
            { name: "Alpaca 🦙", description: "A mild-flavored meat that’s lean, tender, and nutritious, similar to lamb." },
            { name: "Venison 🦌", description: "A flavorful, gamey meat often enjoyed in stews or grilled. It’s rich in protein and low in fat." },
            { name: "Wild Boar 🐗", description: "A dark, rich meat with a bold flavor, perfect for hearty dishes like stews and roasts." },
            { name: "Camel 🐪", description: "A lean and slightly gamey meat, often used in Middle Eastern dishes." },
            { name: "Crocodile 🐊", description: "A mild, white meat often compared to chicken or fish. Great for frying or grilling." }
        ],
        fish: [
            { name: "Tuna 🐟", description: "A meaty fish, perfect for steaks or sushi. Known for its rich flavor and texture." },
            { name: "Swordfish 🗡️🐟", description: "A dense, firm fish with a slightly sweet flavor, often grilled." },
            { name: "Piranha 🐠", description: "A small but flavorful fish, popular in South American cuisines." },
            { name: "Salmon 🐟", description: "A fatty fish with a distinct taste, often smoked, grilled, or baked." },
            { name: "Mahi Mahi 🐟", description: "A mild fish with a slightly sweet flavor, perfect for grilling or sautéing." },
            { name: "Octopus 🐙", description: "Tender and flavorful, this unique seafood is great in soups, salads, and grilled dishes." }
        ],
        plants: [
            { name: "Edible Flowers 🌸", description: "Colorful and aromatic, these flowers add a beautiful touch to salads and desserts." },
            { name: "Wild Herbs 🌿", description: "Fresh, aromatic herbs perfect for garnishing or adding flavor to dishes." },
            { name: "Ginger 🌱", description: "A spicy, aromatic root commonly used in Asian cuisine, known for its health benefits." },
            { name: "Saffron 🌺", description: "A luxurious and fragrant spice, often used in dishes like paella and risotto." },
            { name: "Kale 🥬", description: "A hearty, leafy green packed with nutrients, perfect for soups or salads." }
        ]
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
    const ingredientDescriptions = document.getElementById("ingredientDescriptions");
    const ingredientText = document.getElementById("ingredientText");

    // Functions for adding ingredients
    addMeatButton.addEventListener("click", () => {
        const meat = ingredients.meats[Math.floor(Math.random() * ingredients.meats.length)];
        currentDish.ingredients.push(meat.name);
        ingredientText.innerHTML = `🦘 You added: ${meat.name}. ${meat.description}`;
        ingredientDescriptions.style.display = "block";
    });

    addFishButton.addEventListener("click", () => {
        const fish = ingredients.fish[Math.floor(Math.random() * ingredients.fish.length)];
        currentDish.ingredients.push(fish.name);
        ingredientText.innerHTML = `🐟 You added: ${fish.name}. ${fish.description}`;
        ingredientDescriptions.style.display = "block";
    });

    addPlantButton.addEventListener("click", () => {
        const plant = ingredients.plants[Math.floor(Math.random() * ingredients.plants.length)];
        currentDish.ingredients.push(plant.name);
        ingredientText.innerHTML = `🌿 You added: ${plant.name}. ${plant.description}`;
        ingredientDescriptions.style.display = "block";
    });

    createDishButton.addEventListener("click", () => {
        const name = dishNameInput.value;
        const price = parseFloat(dishPriceInput.value);
        const description = dishDescriptionInput.value;
        const rating = parseInt(dishRatingInput.value);
        
        if (name && price && description && rating) {
            currentDish.name = name;
            currentDish.price = price;
            currentDish.description = description;
            currentDish.rating = rating;
            
            inventory.push(currentDish);
            totalMoney += price;
            updateInventory();
            resetDishInputs();
        }
    });

    // Function to update the inventory display
    function updateInventory() {
        inventoryDiv.innerHTML = "";
        inventory.forEach(dish => {
            const dishCard = document.createElement("div");
            dishCard.classList.add("dish-card");
            dishCard.innerHTML = `
                <div class="dish-title">${dish.name}</div>
                <div class="dish-description">${dish.description}</div>
                <div class="dish-rating">Rating: ${dish.rating} / 5</div>
                <div class="price">Price: $${dish.price.toFixed(2)}</div>
                <button class="sell-button" onclick="sellDish(${dish.price})">Sell</button>
            `;
            inventoryDiv.appendChild(dishCard);
        });
    }

    // Function to sell a dish and earn money
    function sellDish(price) {
        totalMoney += price;
        totalMoneySpan.innerText = totalMoney.toFixed(2);
    }

    // Reset dish inputs after creating a dish
    function resetDishInputs() {
        dishNameInput.value = "";
        dishPriceInput.value = "";
        dishDescriptionInput.value = "";
        dishRatingInput.value = "";
        ingredientDescriptions.style.display = "none";
    }
</script>

</body>
</html>

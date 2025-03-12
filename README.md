<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cooking Adventure</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f3f3f3;
            padding: 20px;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .dish-preview, .inventory, .ingredient-descriptions, .money {
            margin-bottom: 20px;
        }
        .dish-preview div {
            padding: 10px;
            background-color: #fff;
            border: 1px solid #ddd;
            margin-bottom: 10px;
        }
        .ingredient-btns, .create-dish {
            margin-bottom: 20px;
        }
        .ingredient-btns button, .create-dish button {
            padding: 10px 20px;
            margin-right: 10px;
            cursor: pointer;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
        }
        .dish-card {
            background-color: #fff;
            padding: 15px;
            border: 1px solid #ddd;
            margin-bottom: 15px;
        }
        .dish-card button {
            background-color: #f44336;
            color: white;
            border: none;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
        }
        .ingredient-descriptions {
            background-color: #fff;
            padding: 10px;
            display: none;
        }
        .ingredient-descriptions p {
            margin: 5px 0;
        }
        .money {
            font-size: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Cooking Adventure</h1>
        
        <!-- Money Display -->
        <div class="money">
            Total Money: $<span id="totalMoney">0.00</span>
        </div>

        <!-- Ingredient Buttons -->
        <div class="ingredient-btns">
            <button id="addMeatBtn">Add Exotic Meat 🥩</button>
            <button id="addFishBtn">Add Exotic Fish 🐟</button>
            <button id="addPlantBtn">Add Exotic Plant 🌿</button>
        </div>

        <!-- Dish Preview -->
        <div class="dish-preview">
            <h3>Dish Preview</h3>
            <div id="dishName"></div>
            <div id="dishDescription"></div>
            <div id="dishIngredients"></div>
            <div id="dishPrice"></div>
            <div id="dishRating"></div>
        </div>

        <!-- Ingredient Descriptions -->
        <div class="ingredient-descriptions" id="ingredientDescriptions">
            <h4>Ingredient Descriptions:</h4>
            <p id="ingredientDescriptionText"></p>
        </div>

        <!-- Dish Creation -->
        <div class="create-dish">
            <input type="text" id="dishNameInput" placeholder="Dish Name">
            <input type="number" id="dishPriceInput" placeholder="Price">
            <input type="text" id="dishDescriptionInput" placeholder="Dish Description">
            <input type="number" id="dishRatingInput" placeholder="Dish Rating (1-5)">
            <button id="createDishBtn">Create Dish</button>
        </div>

        <!-- Inventory -->
        <div class="inventory">
            <h3>Inventory</h3>
            <div id="inventoryDiv"></div>
        </div>
    </div>

    <script>
        const totalMoneySpan = document.getElementById("totalMoney");
        const dishNameInput = document.getElementById("dishNameInput");
        const dishPriceInput = document.getElementById("dishPriceInput");
        const dishDescriptionInput = document.getElementById("dishDescriptionInput");
        const dishRatingInput = document.getElementById("dishRatingInput");
        const createDishButton = document.getElementById("createDishBtn");
        const addMeatButton = document.getElementById("addMeatBtn");
        const addFishButton = document.getElementById("addFishBtn");
        const addPlantButton = document.getElementById("addPlantBtn");
        const ingredientDescriptions = document.getElementById("ingredientDescriptions");
        const ingredientDescriptionText = document.getElementById("ingredientDescriptionText");
        const inventoryDiv = document.getElementById("inventoryDiv");
        
        let totalMoney = 0;
        const inventory = [];
        let currentDish = {
            name: "",
            price: 0,
            description: "",
            rating: 0,
            ingredients: []
        };

        const ingredients = {
            meat: [
                { name: "Lion Meat", description: "Rare and exotic meat, very tender." },
                { name: "Kangaroo Meat", description: "Lean and flavorful, with a gamey taste." },
            ],
            fish: [
                { name: "Piranha", description: "Dangerous and flavorful fish from the Amazon." },
                { name: "Electric Eel", description: "Shocking and unique fish with a powerful zap." },
            ],
            plants: [
                { name: "Venus Flytrap", description: "A carnivorous plant that adds a spicy twist." },
                { name: "Cactus Fruit", description: "Sweet, tangy, and very rare." },
            ]
        };

        addMeatButton.addEventListener("click", () => {
            const meat = ingredients.meat[Math.floor(Math.random() * ingredients.meat.length)];
            currentDish.ingredients.push(meat.name);
            ingredientDescriptionText.innerHTML = `🥩 You added: ${meat.name}. ${meat.description}`;
            ingredientDescriptions.style.display = "block";
        });

        addFishButton.addEventListener("click", () => {
            const fish = ingredients.fish[Math.floor(Math.random() * ingredients.fish.length)];
            currentDish.ingredients.push(fish.name);
            ingredientDescriptionText.innerHTML = `🐟 You added: ${fish.name}. ${fish.description}`;
            ingredientDescriptions.style.display = "block";
        });

        addPlantButton.addEventListener("click", () => {
            const plant = ingredients.plants[Math.floor(Math.random() * ingredients.plants.length)];
            currentDish.ingredients.push(plant.name);
            ingredientDescriptionText.innerHTML = `🌿 You added: ${plant.name}. ${plant.description}`;
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
                updateDishPreview();
                resetDishInputs();
            }
        });

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
                    <div class="ingredients">Ingredients: ${dish.ingredients.join(", ")}</div>
                    <button onclick="sellDish(${dish.price})">Sell</button>
                `;
                inventoryDiv.appendChild(dishCard);
            });
        }

        function sellDish(price) {
            totalMoney += price;
            totalMoneySpan.innerText = totalMoney.toFixed(2);
        }

        function updateDishPreview() {
            document.getElementById("dishName").innerText = `Name: ${currentDish.name}`;
            document.getElementById("dishDescription").innerText = `Description: ${currentDish.description}`;
            document.getElementById("dishIngredients").innerText = `Ingredients: ${currentDish.ingredients.join(", ")}`;
            document.getElementById("dishPrice").innerText = `Price: $${currentDish.price.toFixed(2)}`;
            document.getElementById("dishRating").innerText = `Rating: ${currentDish.rating} / 5`;
        }

        function resetDishInputs() {
            dishNameInput.value = "";
            dishPriceInput.value = "";
            dishDescriptionInput.value = "";
            dishRatingInput.value = "";
            currentDish.ingredients = [];
            ingredientDescriptions.style.display = "none";
        }
    </script>
</body>
</html>


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cooking Game</title>
    <style>
        /* Basic styling */
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            padding: 20px;
        }
        .button {
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            margin: 10px 0;
        }
        .button:hover {
            background-color: #45a049;
        }
        .inventory-item {
            padding: 10px;
            background-color: #e0e0e0;
            margin: 5px 0;
        }
        .ingredient-description {
            padding: 5px;
            background-color: #f9f9f9;
            border: 1px solid #ccc;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h1>Cooking Game</h1>
    <div>
        <h2>Create Dish</h2>
        <label for="dish-name">Dish Name:</label>
        <input type="text" id="dish-name" placeholder="Enter dish name"><br>
        
        <label for="dish-price">Dish Price ($):</label>
        <input type="number" id="dish-price" placeholder="Enter dish price"><br>

        <label for="dish-description">Dish Description:</label>
        <textarea id="dish-description" placeholder="Enter dish description"></textarea><br>

        <label for="dish-rating">Dish Rating (1-5):</label>
        <input type="number" id="dish-rating" min="1" max="5" placeholder="Enter rating"><br>

        <h3>Add Ingredients:</h3>
        <button class="button" id="add-meat">Add Exotic Meat</button>
        <button class="button" id="add-fish">Add Exotic Fish</button>
        <button class="button" id="add-plant">Add Exotic Plant</button>
        <div id="ingredient-description" class="ingredient-description" style="display:none;"></div>
        <br>
        <button class="button" id="create-dish">Create Dish</button>
    </div>

    <h2>Inventory</h2>
    <button class="button" id="toggle-inventory">Show Inventory</button>
    <div id="inventory" style="display:none;">
        <h3>Dish Inventory</h3>
        <ul id="inventory-list"></ul>
    </div>

    <h3>Total Money: $<span id="total-money">0.00</span></h3>

    <script>
        // Game Variables
        let totalMoney = 0;
        let inventory = [];
        let currentDish = {
            name: '',
            price: 0,
            description: '',
            rating: 0,
            ingredients: []
        };

        // Ingredient Descriptions
        const ingredients = {
            meat: { name: 'Exotic Meat', description: 'A rare and tender cut of meat.' },
            fish: { name: 'Exotic Fish', description: 'A fish found in the deepest parts of the ocean.' },
            plant: { name: 'Exotic Plant', description: 'A rare plant with healing properties.' }
        };

        // DOM Elements
        const totalMoneySpan = document.getElementById('total-money');
        const inventoryList = document.getElementById('inventory-list');
        const dishNameInput = document.getElementById('dish-name');
        const dishPriceInput = document.getElementById('dish-price');
        const dishDescriptionInput = document.getElementById('dish-description');
        const dishRatingInput = document.getElementById('dish-rating');
        const ingredientDescriptionText = document.getElementById('ingredient-description');
        const inventorySection = document.getElementById('inventory');
        const toggleInventoryButton = document.getElementById('toggle-inventory');
        
        // Button Event Listeners
        document.getElementById('add-meat').addEventListener('click', () => addIngredient('meat'));
        document.getElementById('add-fish').addEventListener('click', () => addIngredient('fish'));
        document.getElementById('add-plant').addEventListener('click', () => addIngredient('plant'));
        document.getElementById('create-dish').addEventListener('click', createDish);
        toggleInventoryButton.addEventListener('click', toggleInventory);

        // Functions
        function addIngredient(type) {
            const ingredient = ingredients[type];
            currentDish.ingredients.push(ingredient.name);
            showIngredientDescription(ingredient);
        }

        function showIngredientDescription(ingredient) {
            ingredientDescriptionText.innerHTML = `${ingredient.name}: ${ingredient.description}`;
            ingredientDescriptionText.style.display = "block";
        }

        function createDish() {
            const name = dishNameInput.value;
            const price = parseFloat(dishPriceInput.value);
            const description = dishDescriptionInput.value;
            const rating = parseInt(dishRatingInput.value);

            if (name && price && description && rating >= 1 && rating <= 5 && currentDish.ingredients.length > 0) {
                currentDish.name = name;
                currentDish.price = price;
                currentDish.description = description;
                currentDish.rating = rating;

                inventory.push(currentDish);
                totalMoney += price;

                // Update UI
                updateInventory();
                updateMoney();
                resetDishInputs();
            } else {
                alert('Please complete all fields.');
            }
        }

        function resetDishInputs() {
            dishNameInput.value = '';
            dishPriceInput.value = '';
            dishDescriptionInput.value = '';
            dishRatingInput.value = '';
            currentDish.ingredients = [];
        }

        function updateInventory() {
            inventoryList.innerHTML = '';
            inventory.forEach(dish => {
                const li = document.createElement('li');
                li.classList.add('inventory-item');
                li.innerHTML = `${dish.name} - $${dish.price} <button class="button" onclick="sellDish(${dish.price}, '${dish.name}')">Sell</button>`;
                inventoryList.appendChild(li);
            });
        }

        function sellDish(price, name) {
            totalMoney += price;
            totalMoneySpan.innerText = totalMoney.toFixed(2);

            // Remove the dish from the inventory
            inventory = inventory.filter(dish => dish.name !== name);
            updateInventory();
        }

        function toggleInventory() {
            if (inventorySection.style.display === 'none') {
                inventorySection.style.display = 'block';
                toggleInventoryButton.innerText = 'Hide Inventory';
            } else {
                inventorySection.style.display = 'none';
                toggleInventoryButton.innerText = 'Show Inventory';
            }
        }

        function updateMoney() {
            totalMoneySpan.innerText = totalMoney.toFixed(2);
        }
    </script>
</body>
</html>

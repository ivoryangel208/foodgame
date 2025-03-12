<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dish Creation</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 20px;
            background-color: #f4f4f4;
            color: #333;
        }
        #dish-creation, #inventory {
            background-color: white;
            padding: 20px;
            margin: 20px 0;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        #inventory {
            display: none;
        }
        button {
            padding: 10px 20px;
            margin: 5px;
            background-color: #28a745;
            border: none;
            color: white;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
        #ingredient-description {
            margin-top: 10px;
            font-weight: bold;
        }
        .inventory-item {
            margin-bottom: 10px;
        }
    </style>
</head>
<body>

    <div id="dish-creation">
        <h2>Create Your Dish</h2>
        <input type="text" id="dish-name" placeholder="Enter dish name" />
        <button id="create-dish">Create Dish</button>
        <button id="add-meat">Add Meat</button>
        <button id="add-fish">Add Fish</button>
        <button id="add-plant">Add Plant</button>
        <div id="ingredient-description" style="display:none;"></div>
        <div>
            <h4>Dish Information</h4>
            <p>Name: <span id="dish-name-display"></span></p>
            <p>Price: $<span id="dish-price-display"></span></p>
            <p>Description: <span id="dish-description-display"></span></p>
            <p>Rating: <span id="dish-rating-display"></span> stars</p>
            <p>Ingredients: <span id="dish-ingredients-display"></span></p>
        </div>
    </div>

    <div id="inventory">
        <h2>Dish Inventory</h2>
        <ul id="inventory-list"></ul>
        <button id="sell-dish">Sell Dish</button>
        <button id="toggle-inventory">Toggle Inventory</button>
        <p>Total Money: $<span id="total-money">0.00</span></p>
    </div>

    <script>
        // Data arrays for ingredients and random dish generation
        const dishData = [
            { name: "Spicy Venison Steak", price: 20, description: "A wild, spicy venison steak with a rich flavor, served with roasted vegetables.", rating: 4.5 },
            { name: "Grilled Quail", price: 25, description: "A delicately grilled quail with a sweet glaze and fresh herbs.", rating: 4.8 },
            { name: "Wild Boar Ribs", price: 30, description: "Tender wild boar ribs marinated in a smoky BBQ sauce, perfect for any meat lover.", rating: 4.9 }
        ];
        const exoticMeats = ["Venison", "Goose", "Duck", "Rabbit", "Wild Boar"];
        const exoticFish = ["Swordfish", "Tuna", "Salmon", "Snapper", "Mahi Mahi"];
        const exoticPlants = ["Dragon Fruit", "Durian", "Mangosteen", "Taro", "Kale"];

        let currentDish = { name: '', price: 0, description: '', rating: 0, ingredients: [] };
        let inventory = [];
        let totalMoney = 0;

        // DOM Elements
        const dishNameInput = document.getElementById('dish-name');
        const dishNameDisplay = document.getElementById('dish-name-display');
        const dishPriceDisplay = document.getElementById('dish-price-display');
        const dishDescriptionDisplay = document.getElementById('dish-description-display');
        const dishRatingDisplay = document.getElementById('dish-rating-display');
        const dishIngredientsDisplay = document.getElementById('dish-ingredients-display');
        const ingredientDescriptionText = document.getElementById('ingredient-description');
        const createDishButton = document.getElementById('create-dish');
        const sellDishButton = document.getElementById('sell-dish');
        const inventoryList = document.getElementById('inventory-list');
        const totalMoneySpan = document.getElementById('total-money');
        const toggleInventoryButton = document.getElementById('toggle-inventory');

        // Event Listeners
        document.getElementById('add-meat').addEventListener('click', () => addIngredient('meat'));
        document.getElementById('add-fish').addEventListener('click', () => addIngredient('fish'));
        document.getElementById('add-plant').addEventListener('click', () => addIngredient('plant'));
        createDishButton.addEventListener('click', createDish);
        sellDishButton.addEventListener('click', sellDish);
        toggleInventoryButton.addEventListener('click', toggleInventory);

        // Functions
        function toggleInventory() {
            document.getElementById('inventory').style.display = document.getElementById('inventory').style.display === 'none' ? 'block' : 'none';
        }

        function addIngredient(type) {
            let ingredientsList;
            if (type === 'meat') ingredientsList = exoticMeats;
            else if (type === 'fish') ingredientsList = exoticFish;
            else if (type === 'plant') ingredientsList = exoticPlants;

            const randomIngredient = ingredientsList[Math.floor(Math.random() * ingredientsList.length)];
            currentDish.ingredients.push(randomIngredient);
            ingredientDescriptionText.style.display = 'block';
            ingredientDescriptionText.textContent = `You added: ${randomIngredient}`;
            updateIngredientsDisplay();
        }

        function createDish() {
            if (!dishNameInput.value.trim()) {
                alert("Please name the dish!");
                return;
            }

            const randomDish = dishData[Math.floor(Math.random() * dishData.length)];
            currentDish.name = dishNameInput.value.trim();
            currentDish.price = randomDish.price;
            currentDish.description = randomDish.description;
            currentDish.rating = randomDish.rating;

            dishNameDisplay.textContent = currentDish.name;
            dishPriceDisplay.textContent = currentDish.price;
            dishDescriptionDisplay.textContent = currentDish.description;
            dishRatingDisplay.textContent = currentDish.rating;
            updateIngredientsDisplay();
        }

        function updateIngredientsDisplay() {
            dishIngredientsDisplay.textContent = currentDish.ingredients.join(', ');
        }

        function sellDish() {
            if (currentDish.price === 0) {
                alert("Please create a dish first!");
                return;
            }

            inventory.push({...currentDish});
            totalMoney += currentDish.price;
            totalMoneySpan.textContent = totalMoney.toFixed(2);
            updateInventoryDisplay();
            resetCurrentDish();
        }

        function updateInventoryDisplay() {
            inventoryList.innerHTML = '';
            inventory.forEach(item => {
                const listItem = document.createElement('li');
                listItem.className = 'inventory-item';
                listItem.textContent = `${item.name} - $${item.price} - Rating: ${item.rating} stars`;
                inventoryList.appendChild(listItem);
            });
        }

        function resetCurrentDish() {
            currentDish = { name: '', price: 0, description: '', rating: 0, ingredients: [] };
            dishNameInput.value = '';
            ingredientDescriptionText.style.display = 'none';
            dishIngredientsDisplay.textContent = '';
        }
    </script>
</body>
</html>

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
        <input type="text" id="dish-name" readonly><br>
        
        <label for="dish-price">Dish Price ($):</label>
        <input type="number" id="dish-price" readonly><br>

        <label for="dish-description">Dish Description:</label>
        <textarea id="dish-description" readonly></textarea><br>

        <label for="dish-rating">Dish Rating (1-5):</label>
        <input type="number" id="dish-rating" min="1" max="5" readonly><br>

        <h3>Add Ingredients:</h3>
        <button class="button" id="add-meat">Add Exotic Meat</button>
        <button class="button" id="add-fish">Add Exotic Fish</button>
        <button class="button" id="add-plant">Add Exotic Plant</button>
        <div id="ingredient-description" class="ingredient-description" style="display:none;"></div>
        <br>
        <button class="button" id="create-dish">Create Dish</button>
        <button class="button" id="sell-dish">Sell Dish</button>
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

        // Predefined Dish Data
        const dishData = [
            {name: "Beef Wellington", price: 60, description: "A luxurious dish made of beef fillet, mushroom duxelles, and puff pastry.", rating: 5},
            {name: "Lobster Thermidor", price: 50, description: "A decadent dish featuring lobster, egg yolks, and brandy.", rating: 5},
            {name: "Chicken Parmesan", price: 25, description: "A crispy breaded chicken topped with marinara sauce and melted cheese.", rating: 4},
            {name: "Ratatouille", price: 18, description: "A hearty vegetable stew made from zucchini, eggplant, tomatoes, and bell peppers.", rating: 4},
            {name: "Sushi Platter", price: 35, description: "A selection of fresh sushi with fish like tuna, salmon, and eel.", rating: 5},
            {name: "Boeuf Bourguignon", price: 40, description: "A classic French beef stew braised in red wine with mushrooms and onions.", rating: 5},
            {name: "Pad Thai", price: 20, description: "A stir-fried Thai dish made with rice noodles, shrimp, tofu, peanuts, and lime.", rating: 4},
            {name: "Paella", price: 45, description: "A Spanish rice dish with seafood, saffron, and a mix of vegetables.", rating: 5},
            {name: "Duck à l'Orange", price: 55, description: "Duck breast served with a tangy orange sauce.", rating: 5},
            {name: "Fish Tacos", price: 18, description: "Soft tacos filled with grilled fish, cabbage, and a creamy sauce.", rating: 4},
            {name: "Tom Yum Soup", price: 22, description: "A spicy Thai soup made with shrimp, lemongrass, and chili paste.", rating: 4},
            {name: "Chili Con Carne", price: 20, description: "A spicy stew with beef, chili peppers, beans, and tomatoes.", rating: 3},
            {name: "Steak Frites", price: 30, description: "A simple yet elegant dish featuring a juicy steak and crispy fries.", rating: 5},
            {name: "Tandoori Chicken", price: 25, description: "Chicken marinated in yogurt and spices, then roasted in a tandoor oven.", rating: 4},
            {name: "Fettuccine Alfredo", price: 22, description: "A creamy pasta dish made with butter, cream, and parmesan cheese.", rating: 4},
            {name: "Gyro Plate", price: 18, description: "A Greek dish with seasoned lamb, tzatziki sauce, and pita bread.", rating: 4},
            {name: "Moussaka", price: 30, description: "A Greek casserole with layers of eggplant, ground beef, and béchamel sauce.", rating: 5},
            {name: "Peking Duck", price: 50, description: "A famous Chinese dish featuring crispy duck skin and tender meat.", rating: 5},
            {name: "Gumbo", price: 28, description: "A rich and flavorful stew with sausage, seafood, and okra.", rating: 4},
            {name: "Vegetable Tempura", price: 15, description: "Crispy battered vegetables, often served with a soy-based dipping sauce.", rating: 3}
        ];

        // Ingredients Lists
        const exoticMeats = ["Venison", "Bison", "Kangaroo", "Camel", "Alligator", "Ostrich", "Pigeon", "Boar", "Frog Legs", "Elk", "Yak", "Zebra", "Crocodile", "Antelope", "Wild Boar", "Guinea Fowl", "Quail", "Pheasant", "Rabbit", "Swan"];
        const exoticFish = ["Swordfish", "Tuna", "Bluefin Tuna", "Halibut", "King Salmon", "Sturgeon", "Mahi Mahi", "Wahoo", "Bass", "Pike", "Barracuda", "Snapper", "Swordfish", "Flounder", "Tilapia", "Anchovy", "Herring", "Pollock", "Sardines", "Chilean Sea Bass"];
        const exoticPlants = ["Truffle", "Saffron", "Wasabi", "Coriander", "Fennel", "Kaffir Lime", "Mango Leaves", "Dragon Fruit", "Durian", "Ginseng", "Bamboo Shoots", "Elderflower", "Lavender", "Chili Pepper", "Cilantro", "Lemongrass", "Turmeric", "Lime Zest", "Coconut", "Mint"];

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
        document.getElementById('sell-dish').addEventListener('click', sellDish);
        toggleInventoryButton.addEventListener('click', toggleInventory);

        // Functions
        function addIngredient(type) {
            let ingredientList = [];
            let ingredientType = '';
            if (type === 'meat') {
                ingredientList = exoticMeats;
                ingredientType = 'Meat';
            } else if (type === 'fish') {
                ingredientList = exoticFish;
                ingredientType = 'Fish';
            } else if (type === 'plant') {
                ingredientList = exoticPlants;
                ingredientType = 'Plant';
            }
            
            // Randomly pick an ingredient
            const randomIngredient = ingredientList[Math.floor(Math.random() * ingredientList.length)];
            currentDish.ingredients.push(randomIngredient);
            ingredientDescriptionText.textContent = `${ingredientType} Added: ${randomIngredient}`;
            ingredientDescriptionText.style.display = 'block';
        }

        function createDish() {
            // Select a random dish from the predefined list
            const randomDish = dishData[Math.floor(Math.random() * dishData.length)];
            currentDish.name = randomDish.name;
            currentDish.price = randomDish.price;
            currentDish.description = randomDish.description;
            currentDish.rating = randomDish.rating;

            // Update the inputs
            dishNameInput.value = currentDish.name;
            dishPriceInput.value = currentDish.price;
            dishDescriptionInput.value = currentDish.description;
            dishRatingInput.value = currentDish.rating;
        }

        function sellDish() {
            // Add the current dish to inventory and update total money
            inventory.push(currentDish);
            totalMoney += currentDish.price;
            updateMoney();
            currentDish = { name: '', price: 0, description: '', rating: 0, ingredients: [] };
            alert("Dish Sold!");

            // Update the inventory list
            updateInventory();
        }

        function updateInventory() {
            inventoryList.innerHTML = '';
            inventory.forEach(dish => {
                const li = document.createElement('li');
                li.classList.add('inventory-item');
                li.textContent = `${dish.name} - $${dish.price} | Rating: ${dish.rating} | Ingredients: ${dish.ingredients.join(', ')}`;
                inventoryList.appendChild(li);
            });
        }

        function updateMoney() {
            totalMoneySpan.textContent = totalMoney.toFixed(2);
        }

        function toggleInventory() {
            inventorySection.style.display = (inventorySection.style.display === 'none') ? 'block' : 'none';
        }
    </script>
</body>
</html>

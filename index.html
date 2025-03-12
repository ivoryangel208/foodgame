<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cooking Game</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f4f9;
            color: #333;
            padding: 20px;
            margin: 0;
            box-sizing: border-box;
        }

        h1 {
            text-align: center;
            font-size: 36px;
            margin-bottom: 20px;
            color: #4CAF50;
        }

        h2 {
            font-size: 28px;
            color: #444;
            margin-bottom: 10px;
        }

        .section {
            background-color: #fff;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
        }

        .button {
            padding: 12px 25px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
            margin: 5px;
        }

        .button:hover {
            background-color: #45a049;
        }

        .button:active {
            background-color: #3e8e41;
        }

        input, textarea {
            width: 100%;
            padding: 10px;
            margin-top: 8px;
            border-radius: 5px;
            border: 1px solid #ddd;
            font-size: 16px;
            margin-bottom: 15px;
        }

        input[readonly], textarea[readonly] {
            background-color: #f9f9f9;
        }

        #ingredient-description {
            font-size: 16px;
            margin-top: 10px;
            padding: 10px;
            background-color: #e9f7e7;
            border: 1px solid #d4e4d1;
            border-radius: 5px;
            display: none;
        }

        .inventory-item {
            background-color: #e9f7e7;
            padding: 10px;
            margin: 5px 0;
            border-radius: 5px;
        }

        .inventory {
            padding: 20px;
            margin-top: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        #total-money {
            font-size: 24px;
            font-weight: bold;
            color: #4CAF50;
        }

        .dish-info {
            margin-bottom: 15px;
        }

        .dish-info h3 {
            font-size: 20px;
            margin-bottom: 5px;
        }

        .inventory-list {
            padding-left: 20px;
        }

        .inventory-list li {
            font-size: 16px;
        }

        #inventory {
            display: none;
        }
    </style>
</head>
<body>
    <h1>Cooking Game</h1>
    
    <div class="section">
        <h2>Create Dish</h2>
        <div class="dish-info">
            <h3>Dish Name:</h3>
            <input type="text" id="dish-name" readonly>
        </div>
        <div class="dish-info">
            <h3>Dish Price ($):</h3>
            <input type="number" id="dish-price" readonly>
        </div>
        <div class="dish-info">
            <h3>Dish Description:</h3>
            <textarea id="dish-description" readonly></textarea>
        </div>
        <div class="dish-info">
            <h3>Dish Rating (1-5):</h3>
            <input type="number" id="dish-rating" min="1" max="5" readonly>
        </div>
        
        <h3>Add Ingredients:</h3>
        <button class="button" id="add-meat">Add Exotic Meat</button>
        <button class="button" id="add-fish">Add Exotic Fish</button>
        <button class="button" id="add-plant">Add Exotic Plant</button>
        
        <div id="ingredient-description"></div>
        
        <br>
        <button class="button" id="create-dish">Create Dish</button>
        <button class="button" id="sell-dish">Sell Dish</button>
    </div>

    <div class="section inventory">
        <h2>Inventory</h2>
        <button class="button" id="toggle-inventory">Show Inventory</button>
        <ul id="inventory-list" class="inventory-list"></ul>
        <h3>Total Money: $<span id="total-money">0.00</span></h3>
    </div>

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
        const exoticMeats = ["Venison", "Bison", "Kangaroo", "Camel", "Alligator", "Ostrich", "Pigeon", "Boar", "Frog Legs", "Elk", "Wagyu Beef", "Goose", "Duck", "Quail", "Rabbit", "Wild Turkey", "Buffalo", "Squirrel", "Wild Boar", "Reindeer"];
        const exoticFish = ["Swordfish", "Tuna", "Salmon", "Snapper", "Mahi Mahi", "Yellowtail", "Barracuda", "Halibut", "Grouper", "Octopus", "Scallops", "Sea Bass", "Tilapia", "Caviar", "Abalone", "King Crab", "Lobster", "Rockfish", "Eel", "Shrimp"];
        const exoticPlants = ["Dragon Fruit", "Durian", "Mangosteen", "Taro", "Kale", "Wasabi", "Sichuan Pepper", "Fiddlehead Fern", "Cucumber", "Coriander", "Yams", "Okra", "Bamboo Shoots", "Lotus Root", "Jalapeño", "Chili Peppers", "Fennel", "Artichokes", "Squash", "Sweet Potatoes"];

        // DOM Elements
        const dishNameInput = document.getElementById('dish-name');
        const dishPriceInput = document.getElementById('dish-price');
        const dishDescriptionInput = document.getElementById('dish-description');
        const dishRatingInput = document.getElementById('dish-rating');
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
        }

        function createDish() {
            const randomDish = dishData[Math.floor(Math.random() * dishData.length)];
            currentDish.name = randomDish.name;
            currentDish.price = randomDish.price;
            currentDish.description = randomDish.description;
            currentDish.rating = randomDish.rating;

            dishNameInput.value = currentDish.name;
            dishPriceInput.value = currentDish.price;
            dishDescriptionInput.value = currentDish.description;
            dishRatingInput.value = currentDish.rating;
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
            dishPriceInput.value = '';
            dishDescriptionInput.value = '';
            dishRatingInput.value = '';
            ingredientDescriptionText.style.display = 'none';
        }
    </script>
</body>
</html>

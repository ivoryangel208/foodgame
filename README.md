<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dish Creation Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            padding: 20px;
        }
        button {
            padding: 10px;
            margin: 5px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .dish-list {
            margin-top: 20px;
        }
        .dish {
            background-color: #e0e0e0;
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <h1>Dish Creation Game</h1>
    <label for="dish-name">Dish Name:</label>
    <input type="text" id="dish-name" placeholder="Enter dish name" />
    <button id="create-dish">Create Dish</button>
    <button id="view-inventory">View Inventory</button>

    <div id="ingredient-section">
        <button id="add-meat">Add Meat</button>
        <button id="add-fish">Add Fish</button>
        <button id="add-plant">Add Plant</button>
        <button id="add-fruit">Add Fruit</button>
        <button id="add-veg">Add Veggie</button>
    </div>

    <div id="dish-list" class="dish-list"></div>
    <div id="inventory" style="display: none;">
        <h3>Inventory</h3>
        <div id="inventory-list"></div>
    </div>

    <script>
        // Define ingredients
        const meats = ["Beef", "Chicken", "Pork", "Lamb", "Venison", "Rabbit", "Goat", "Duck", "Bison", "Kangaroo", "Turkey", "Boar", "Elk", "Emu", "Ostrich", "Quail", "Pheasant", "Goose", "Sausage", "Pastrami", "Salami", "Pepperoni", "Jerky", "T-bone steak", "Ribs", "Liver", "Lamb chops", "Chicken wings", "Chicken breast", "Chicken thighs"];
        const fishes = ["Salmon", "Tuna", "Trout", "Cod", "Herring", "Sardine", "Mackerel", "Swordfish", "Halibut", "Bass", "Pike", "Catfish", "Perch", "Shark", "Anchovy", "Tilapia", "Eel", "Walleye", "Flounder", "Pollock", "Clams", "Mussels", "Shrimp", "Crab", "Lobster", "Scallops", "Oysters", "Octopus", "Squid", "Caviar", "Sea bass"];
        const plants = ["Carrot", "Potato", "Spinach", "Tomato", "Broccoli", "Cabbage", "Lettuce", "Cauliflower", "Onion", "Garlic", "Peppers", "Zucchini", "Squash", "Pumpkin", "Eggplant", "Beets", "Asparagus", "Radish", "Artichoke", "Kale", "Brussels sprouts", "Chard", "Sweet potato", "Cucumber", "Green beans", "Celery", "Leeks", "Parsnips", "Mushrooms", "Fennel", "Turnips"];
        const fruits = ["Apple", "Banana", "Strawberry", "Orange", "Grapes", "Mango", "Pineapple", "Peach", "Plum", "Kiwi", "Cherry", "Blueberry", "Raspberry", "Blackberry", "Papaya", "Watermelon", "Cantaloupe", "Lemon", "Lime", "Grapefruit", "Pear", "Pomegranate", "Fig", "Apricot", "Dragonfruit", "Passionfruit", "Lychee", "Tangerine", "Starfruit", "Guava", "Coconut"];
        const veggies = ["Corn", "Beets", "Lettuce", "Celery", "Carrot", "Peas", "Potatoes", "Brussels sprouts", "Sweet corn", "Bell pepper", "Tomatoes", "Asparagus", "Cabbage", "Cauliflower", "Cucumber", "Spinach", "Zucchini", "Leeks", "Kale", "Chard", "Radishes", "Arugula", "Rutabaga", "Turnip", "Okra", "Chili pepper", "Fennel", "Onion", "Garlic", "Shallots", "Chives"];

        const descriptions = [
            "A hearty and delicious dish.",
            "A unique blend of flavors.",
            "A fresh, healthy choice.",
            "A comfort food favorite.",
            "A spicy and bold combination.",
            "A light and refreshing dish."
        ];

        const pricesPerIngredient = {
            "Beef": 15, "Chicken": 10, "Pork": 12, "Lamb": 18, "Venison": 25, "Rabbit": 20, "Goat": 22, "Duck": 30, "Bison": 35, "Kangaroo": 28,
            "Salmon": 20, "Tuna": 22, "Trout": 18, "Cod": 15, "Herring": 10, "Sardine": 8, "Mackerel": 15, "Swordfish": 25, "Halibut": 22, "Bass": 18,
            "Carrot": 2, "Potato": 3, "Spinach": 4, "Tomato": 5, "Broccoli": 6, "Cabbage": 4, "Lettuce": 3, "Cauliflower": 5, "Onion": 2, "Garlic": 1,
            "Apple": 4, "Banana": 3, "Strawberry": 6, "Orange": 5, "Grapes": 7, "Mango": 8, "Pineapple": 10, "Peach": 6, "Plum": 5, "Kiwi": 5,
            "Corn": 4, "Beets": 3, "Lettuce": 3, "Celery": 2, "Carrot": 2, "Peas": 3, "Potatoes": 3, "Brussels sprouts": 5, "Sweet corn": 4, "Bell pepper": 4
        };

        let inventory = [];
        let currentDish = null;

        const dishNameInput = document.getElementById('dish-name');
        const createDishButton = document.getElementById('create-dish');
        const viewInventoryButton = document.getElementById('view-inventory');
        const addMeatButton = document.getElementById('add-meat');
        const addFishButton = document.getElementById('add-fish');
        const addPlantButton = document.getElementById('add-plant');
        const addFruitButton = document.getElementById('add-fruit');
        const addVegButton = document.getElementById('add-veg');
        const dishList = document.getElementById('dish-list');
        const inventoryList = document.getElementById('inventory-list');
        const inventorySection = document.getElementById('inventory');

        // Create Dish
        createDishButton.addEventListener('click', function () {
            const dishName = dishNameInput.value;
            if (dishName === "") {
                alert("Please enter a dish name.");
                return;
            }

            // Initialize a new dish with no ingredients
            const dish = {
                name: dishName,
                ingredients: [],
                price: 0,
                description: descriptions[Math.floor(Math.random() * descriptions.length)],
                rating: Math.floor(Math.random() * 5) + 1
            };

            currentDish = dish;
            updateDishDisplay();
            dishNameInput.value = "";
        });

        // Add ingredients to current dish
        addMeatButton.addEventListener('click', function () {
            addIngredient(meats, "meat");
        });

        addFishButton.addEventListener('click', function () {
            addIngredient(fishes, "fish");
        });

        addPlantButton.addEventListener('click', function () {
            addIngredient(plants, "plant");
        });

        addFruitButton.addEventListener('click', function () {
            addIngredient(fruits, "fruit");
        });

        addVegButton.addEventListener('click', function () {
            addIngredient(veggies, "veg");
        });

        function addIngredient(ingredientArray, type) {
            if (!currentDish) {
                alert("Please create a dish first.");
                return;
            }
            const randomIngredient = ingredientArray[Math.floor(Math.random() * ingredientArray.length)];
            currentDish.ingredients.push(randomIngredient);
            updateDishPrice();
            updateDishDisplay();
        }

        // Update dish price based on ingredients
        function updateDishPrice() {
            currentDish.price = currentDish.ingredients.reduce((total, ingredient) => total + (pricesPerIngredient[ingredient] || 0), 0);
        }

        // Update the dish display
        function updateDishDisplay() {
            if (!currentDish) return;
            const dishDiv = document.createElement('div');
            dishDiv.className = "dish";
            dishDiv.innerHTML = `<strong>${currentDish.name}</strong><br>
                                Description: ${currentDish.description}<br>
                                Ingredients: ${currentDish.ingredients.join(', ')}<br>
                                Price: $${currentDish.price}<br>
                                Rating: ${currentDish.rating} stars`;

            dishList.innerHTML = '';
            dishList.appendChild(dishDiv);
        }

        // View Inventory
        viewInventoryButton.addEventListener('click', function () {
            inventorySection.style.display = inventorySection.style.display === "none" ? "block" : "none";
            inventoryList.innerHTML = inventory.join('<br>');
        });
    </script>

</body>
</html>


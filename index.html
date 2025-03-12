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
    </div>

    <div id="dish-list" class="dish-list"></div>
    <div id="inventory" style="display: none;">
        <h3>Inventory</h3>
        <div id="inventory-list"></div>
    </div>

    <script>
        const meats = ["Beef", "Chicken", "Pork", "Lamb"];
        const fishes = ["Salmon", "Tuna", "Trout", "Cod"];
        const plants = ["Carrot", "Potato", "Spinach", "Tomato"];

        const descriptions = [
            "A hearty and delicious dish.",
            "A unique blend of flavors.",
            "A fresh, healthy choice.",
            "A comfort food favorite."
        ];
        const prices = [10, 15, 20, 25];
        const ratings = [1, 2, 3, 4, 5];

        let inventory = [];
        let currentDish = null;

        const dishNameInput = document.getElementById('dish-name');
        const createDishButton = document.getElementById('create-dish');
        const viewInventoryButton = document.getElementById('view-inventory');
        const addMeatButton = document.getElementById('add-meat');
        const addFishButton = document.getElementById('add-fish');
        const addPlantButton = document.getElementById('add-plant');
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

            // Randomly assign price, description, and rating
            const price = prices[Math.floor(Math.random() * prices.length)];
            const description = descriptions[Math.floor(Math.random() * descriptions.length)];
            const rating = ratings[Math.floor(Math.random() * ratings.length)];

            const dish = {
                name: dishName,
                price: price,
                description: description,
                rating: rating,
                ingredients: []
            };

            currentDish = dish;

            // Display the dish creation UI
            const dishDiv = document.createElement('div');
            dishDiv.classList.add('dish');
            dishDiv.innerHTML = `
                <strong>${dish.name}</strong><br>
                Price: $${price}<br>
                Rating: ${rating} stars<br>
                Description: ${description}<br>
                Ingredients: ${dish.ingredients.join(', ') || "None"}<br>
                <button onclick="sellDish(${price})">Sell for $${price}</button>
            `;
            dishList.appendChild(dishDiv);

            // Reset the input field
            dishNameInput.value = "";
        });

        // Add ingredients to current dish
        addMeatButton.addEventListener('click', function () {
            addIngredient(meats);
        });

        addFishButton.addEventListener('click', function () {
            addIngredient(fishes);
        });

        addPlantButton.addEventListener('click', function () {
            addIngredient(plants);
        });

        function addIngredient(ingredientArray) {
            if (!currentDish) {
                alert("Please create a dish first.");
                return;
            }
            const randomIngredient = ingredientArray[Math.floor(Math.random() * ingredientArray.length)];
            currentDish.ingredients.push(randomIngredient);

            // Update the dish display with new ingredients
            const dishDiv = dishList.querySelector('.dish');
            dishDiv.innerHTML = `
                <strong>${currentDish.name}</strong><br>
                Price: $${currentDish.price}<br>
                Rating: ${currentDish.rating} stars<br>
                Description: ${currentDish.description}<br>
                Ingredients: ${currentDish.ingredients.join(', ')}<br>
                <button onclick="sellDish(${currentDish.price})">Sell for $${currentDish.price}</button>
            `;
        }

        // Sell the dish
        function sellDish(price) {
            inventory.push(currentDish);
            alert("Dish sold! You earned $" + price);
            displayInventory();
        }

        // View inventory
        viewInventoryButton.addEventListener('click', function () {
            inventorySection.style.display = inventorySection.style.display === "none" ? "block" : "none";
        });

        // Display inventory
        function displayInventory() {
            inventoryList.innerHTML = "";
            inventory.forEach(dish => {
                const dishDiv = document.createElement('div');
                dishDiv.innerHTML = `
                    <strong>${dish.name}</strong><br>
                    Price: $${dish.price}<br>
                    Rating: ${dish.rating} stars<br>
                    Description: ${dish.description}<br>
                    Ingredients: ${dish.ingredients.join(", ")}
                `;
                inventoryList.appendChild(dishDiv);
            });
        }
    </script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dish Creation Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f4f4f4;
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
        .dish-list, .inventory {
            margin-top: 20px;
        }
        .dish, .inventory-item {
            margin: 10px;
            padding: 10px;
            background-color: #f9f9f9;
            border-radius: 5px;
        }
        .inventory {
            display: none;
        }
    </style>
</head>
<body>

    <h1>Dish Creation Game</h1>
    <input type="text" id="dish-name" placeholder="Enter dish name" />
    <button id="create-dish">Create Dish</button>
    <button id="inventory-btn">View Inventory</button>
    <div id="ingredient-section">
        <button id="add-meat">Add Meat</button>
        <button id="add-fish">Add Fish</button>
        <button id="add-plant">Add Plant</button>
    </div>

    <div id="dish-list" class="dish-list"></div>
    <div id="inventory" class="inventory">
        <h3>Inventory</h3>
        <div id="inventory-items"></div>
    </div>

    <script>
        // Predefined data for ingredients, prices, ratings, and descriptions
        const meats = ["Beef", "Chicken", "Pork", "Lamb", "Venison"];
        const fishes = ["Salmon", "Tuna", "Trout", "Cod", "Mackerel"];
        const plants = ["Carrot", "Potato", "Spinach", "Lettuce", "Tomato"];

        const descriptions = [
            "A hearty and delicious dish.",
            "A unique blend of flavors.",
            "A fresh, healthy choice.",
            "A comfort food favorite.",
            "A spicy, bold dish."
        ];
        const prices = [10, 15, 20, 25, 30];
        const ratings = [1, 2, 3, 4, 5];

        let inventory = [];
        let earnings = 0;

        // Elements
        const dishNameInput = document.getElementById('dish-name');
        const createDishButton = document.getElementById('create-dish');
        const inventoryButton = document.getElementById('inventory-btn');
        const ingredientSection = document.getElementById('ingredient-section');
        const dishList = document.getElementById('dish-list');
        const inventorySection = document.getElementById('inventory');
        const inventoryItems = document.getElementById('inventory-items');

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

            const ingredients = [];

            const dish = {
                name: dishName,
                price: price,
                description: description,
                rating: rating,
                ingredients: ingredients
            };

            // Create and display the dish
            const dishDiv = document.createElement('div');
            dishDiv.classList.add('dish');
            dishDiv.innerHTML = `
                <strong>${dishName}</strong><br>
                Price: $${price}<br>
                Rating: ${rating} stars<br>
                Description: ${description}<br>
                Ingredients: ${ingredients.join(', ') || "None"}<br>
                <button onclick="sellDish(${price})">Sell for $${price}</button>
            `;

            dishList.appendChild(dishDiv);
            dishNameInput.value = ""; // Reset input field
        });

        // Add ingredient functions
        document.getElementById('add-meat').addEventListener('click', function () {
            addIngredient(meats, "meat");
        });
        document.getElementById('add-fish').addEventListener('click', function () {
            addIngredient(fishes, "fish");
        });
        document.getElementById('add-plant').addEventListener('click', function () {
            addIngredient(plants, "plant");
        });

        function addIngredient(ingredientArray, type) {
            const dishName = dishNameInput.value;
            if (!dishName) {
                alert("Please create a dish first.");
                return;
            }
            const randomIngredient = ingredientArray[Math.floor(Math.random() * ingredientArray.length)];

            // Find the created dish by name
            const dish = Array.from(dishList.children).find(dish => dish.querySelector('strong').textContent === dishName);

            // Add the ingredient to the dish's ingredients array and display it
            if (dish) {
                const ingredientsList = dish.querySelector('Ingredients');
                if (ingredientsList) {
                    ingredientsList.textContent += `, ${randomIngredient}`;
                } else {
                    dish.innerHTML += `Ingredients: ${randomIngredient}<br>`;
                }
            }
        }

        // Sell Dish Function
        function sellDish(price) {
            earnings += price;
            alert("Dish sold! You earned $" + price);
            displayEarnings();
        }

        function displayEarnings() {
            alert("Total Earnings: $" + earnings);
        }

        // View Inventory
        inventoryButton.addEventListener('click', function () {
            inventorySection.style.display = inventorySection.style.display === "none" ? "block" : "none";
        });

        // Displaying all dishes in the inventory
        function displayInventory() {
            inventoryItems.innerHTML = "";
            inventory.forEach(dish => {
                const dishDiv = document.createElement('div');
                dishDiv.classList.add('inventory-item');
                dishDiv.innerHTML = `
                    <strong>${dish.name}</strong><br>
                    Price: $${dish.price}<br>
                    Rating: ${dish.rating} stars<br>
                    Description: ${dish.description}<br>
                    Ingredients: ${dish.ingredients.join(", ")}
                `;
                inventoryItems.appendChild(dishDiv);
            });
        }
    </script>
</body>
</html>

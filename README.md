<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dish Creation Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f8ff; /* Light blue background for calming effect */
            color: #333;
            padding: 20px;
            margin: 0;
        }
        h1, h3, h4 {
            color: #5a9ab5; /* Soft teal for headings */
            text-align: center;
        }
        input, button {
            font-size: 16px;
            padding: 10px;
            margin: 5px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        button {
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .ingredient-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 10px;
            margin-bottom: 20px;
        }
        .ingredient-list button {
            background-color: #f1f1f1;
            border: 1px solid #ddd;
            padding: 8px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .ingredient-list button:hover {
            background-color: #e0e0e0;
        }
        .dish-list {
            margin-top: 20px;
            background-color: #fff;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .dish {
            background-color: #e9f7f6;
            border: 1px solid #d0d0d0;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <h1>Dish Creation Game</h1>
    <label for="dish-name">Dish Name:</label>
    <input type="text" id="dish-name" placeholder="Enter dish name" />
    <button id="create-dish">Create Dish</button>
    
    <h3>Choose Ingredients for Your Dish</h3>

    <!-- Meats Section -->
    <div id="meat-section" class="ingredient-list">
        <h4>Meats:</h4>
    </div>
    
    <!-- Fishes Section -->
    <div id="fish-section" class="ingredient-list">
        <h4>Fishes:</h4>
    </div>
    
    <!-- Plants Section -->
    <div id="plant-section" class="ingredient-list">
        <h4>Plants:</h4>
    </div>
    
    <!-- Fruits Section -->
    <div id="fruit-section" class="ingredient-list">
        <h4>Fruits:</h4>
    </div>
    
    <!-- Veggies Section -->
    <div id="veg-section" class="ingredient-list">
        <h4>Veggies:</h4>
    </div>

    <button id="view-dish">View Dish</button>

    <div id="dish-list" class="dish-list"></div>

    <script>
        // Define ingredients (with added ones)
        const meats = [
            "Beef", "Chicken", "Pork", "Lamb", "Venison", "Rabbit", "Goat", "Duck", "Bison", "Kangaroo", 
            "Turkey", "Boar", "Elk", "Emu", "Ostrich", "Quail", "Pheasant", "Goose", "Sausage", "Pastrami", 
            "Salami", "Pepperoni", "Jerky", "T-bone steak", "Ribs", "Liver", "Lamb chops", "Chicken wings", 
            "Chicken breast", "Chicken thighs", "Duck breast", "Pork belly", "Ribeye", "Filet mignon", "Ground beef"
        ];
        const fishes = [
            "Salmon", "Tuna", "Trout", "Cod", "Herring", "Sardine", "Mackerel", "Swordfish", "Halibut", "Bass", 
            "Pike", "Catfish", "Perch", "Shark", "Anchovy", "Tilapia", "Eel", "Walleye", "Flounder", "Pollock", 
            "Clams", "Mussels", "Shrimp", "Crab", "Lobster", "Scallops", "Oysters", "Octopus", "Squid", "Caviar", 
            "Sea bass", "Barracuda", "Snapper", "Mahi Mahi", "Sea trout"
        ];
        const plants = [
            "Carrot", "Potato", "Spinach", "Tomato", "Broccoli", "Cabbage", "Lettuce", "Cauliflower", "Onion", 
            "Garlic", "Peppers", "Zucchini", "Squash", "Pumpkin", "Eggplant", "Beets", "Asparagus", "Radish", 
            "Artichoke", "Kale", "Brussels sprouts", "Chard", "Sweet potato", "Cucumber", "Green beans", "Celery", 
            "Leeks", "Parsnips", "Mushrooms", "Fennel", "Turnips", "Olives", "Chili peppers", "Okra", "Taro root"
        ];
        const fruits = [
            "Apple", "Banana", "Strawberry", "Orange", "Grapes", "Mango", "Pineapple", "Peach", "Plum", "Kiwi", 
            "Cherry", "Blueberry", "Raspberry", "Blackberry", "Papaya", "Watermelon", "Cantaloupe", "Lemon", "Lime", 
            "Grapefruit", "Pear", "Pomegranate", "Fig", "Apricot", "Dragonfruit", "Passionfruit", "Lychee", 
            "Tangerine", "Starfruit", "Guava", "Coconut", "Durian", "Jackfruit", "Persimmon", "Mulberry"
        ];
        const veggies = [
            "Corn", "Beets", "Lettuce", "Celery", "Carrot", "Peas", "Potatoes", "Brussels sprouts", "Sweet corn", 
            "Bell pepper", "Tomatoes", "Asparagus", "Cabbage", "Cauliflower", "Cucumber", "Spinach", "Zucchini", 
            "Leeks", "Kale", "Chard", "Radishes", "Arugula", "Rutabaga", "Turnip", "Okra", "Chili pepper", 
            "Fennel", "Onion", "Garlic", "Shallots", "Chives", "Watercress", "Endive", "Bok choy", "Mustard greens"
        ];

        const descriptions = [
            "A hearty and delicious dish.",
            "A unique blend of flavors.",
            "A fresh, healthy choice.",
            "A comfort food favorite.",
            "A spicy and bold combination.",
            "A light and refreshing dish."
        ];

        const pricesPerIngredient = {
            "Beef": 15, "Chicken": 10, "Pork": 12, "Lamb": 18, "Venison": 25, "Rabbit": 20, "Goat": 22, "Duck": 30, 
            "Bison": 35, "Kangaroo": 28, "Salmon": 20, "Tuna": 22, "Trout": 18, "Cod": 15, "Herring": 10, "Sardine": 8, 
            "Mackerel": 15, "Swordfish": 25, "Halibut": 22, "Bass": 18, "Carrot": 2, "Potato": 3, "Spinach": 4, 
            "Tomato": 5, "Broccoli": 6, "Cabbage": 4, "Lettuce": 3, "Cauliflower": 5, "Onion": 2, "Garlic": 1, 
            "Apple": 4, "Banana": 3, "Strawberry": 6, "Orange": 5, "Grapes": 7, "Mango": 8, "Pineapple": 10, "Peach": 6,
            "Corn": 4, "Beets": 3, "Lettuce": 3, "Celery": 2, "Carrot": 2, "Peas": 3, "Potatoes": 3, "Brussels sprouts": 5,
            "Bell pepper": 4, "Tomatoes": 3
        };

        // Add ingredients to their respective sections
        const addIngredients = (sectionId, ingredients) => {
            const section = document.getElementById(sectionId);
            section.innerHTML = ingredients.map(item => `<button class="ingredient">${item}</button>`).join('');
        };

        addIngredients("meat-section", meats);
        addIngredients("fish-section", fishes);
        addIngredients("plant-section", plants);
        addIngredients("fruit-section", fruits);
        addIngredients("veg-section", veggies);

        // Function to calculate the price of selected ingredients
        const calculatePrice = () => {
            let totalPrice = 0;
            const selectedIngredients = document.querySelectorAll(".selected");
            selectedIngredients.forEach(ingredient => {
                const price = pricesPerIngredient[ingredient.textContent];
                totalPrice += price;
            });
            return totalPrice;
        };

        // Handling ingredient selection
        document.querySelectorAll('.ingredient').forEach(button => {
            button.addEventListener('click', () => {
                button.classList.toggle('selected');
                document.getElementById('create-dish').disabled = false;
            });
        });

        // Creating the dish
        document.getElementById("create-dish").addEventListener('click', () => {
            const dishName = document.getElementById("dish-name").value;
            const selectedIngredients = document.querySelectorAll(".selected");
            const ingredientsList = Array.from(selectedIngredients).map(ingredient => ingredient.textContent).join(', ');
            const price = calculatePrice();
            const description = descriptions[Math.floor(Math.random() * descriptions.length)];

            const dishHTML = `
                <div class="dish">
                    <h4>${dishName || "Untitled Dish"}</h4>
                    <p><strong>Ingredients:</strong> ${ingredientsList || "No ingredients selected"}</p>
                    <p><strong>Description:</strong> ${description}</p>
                    <p><strong>Price:</strong> $${price}</p>
                </div>
            `;

            document.getElementById("dish-list").innerHTML = dishHTML;
            document.getElementById("create-dish").disabled = true; // Disable the button after creating the dish
        });
    </script>

</body>
</html>

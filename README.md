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
            "Chicken breast", "Chicken thighs", "Duck breast", "Pork belly", "Ribeye", "Filet mignon", "Ground beef",
            "Bacon", "Pork shoulder", "Beef brisket", "Short ribs", "Chorizo", "Mutton", "Tri-tip", "Flank steak", 
            "Steak tips", "Chicken legs", "Chicken drumsticks", "Brisket", "Liverwurst", "Lamb leg", "Pulled pork", 
            "Roast beef", "Corned beef", "Pork ribs"
        ];
        const fishes = [
            "Salmon", "Tuna", "Trout", "Cod", "Herring", "Sardine", "Mackerel", "Swordfish", "Halibut", "Bass", 
            "Pike", "Catfish", "Perch", "Shark", "Anchovy", "Tilapia", "Eel", "Walleye", "Flounder", "Pollock", 
            "Clams", "Mussels", "Shrimp", "Crab", "Lobster", "Scallops", "Oysters", "Octopus", "Squid", "Caviar", 
            "Sea bass", "Barracuda", "Snapper", "Mahi Mahi", "Sea trout", "Chilean sea bass", "Red snapper", 
            "Scampi", "Mullet", "Tilapia", "Swordfish", "Kingfish", "Anchovy", "Pompano", "Langoustine", "Turbot",
            "Arctic char", "Amberjack", "Flounder", "Seabream", "John Dory"
        ];
        const plants = [
            "Carrot", "Potato", "Spinach", "Tomato", "Broccoli", "Cabbage", "Lettuce", "Cauliflower", "Onion", 
            "Garlic", "Peppers", "Zucchini", "Squash", "Pumpkin", "Eggplant", "Beets", "Asparagus", "Radish", 
            "Artichoke", "Kale", "Brussels sprouts", "Chard", "Sweet potato", "Cucumber", "Green beans", "Celery", 
            "Leeks", "Parsnips", "Mushrooms", "Fennel", "Turnips", "Olives", "Chili peppers", "Okra", "Taro root", 
            "Nori", "Algae", "Bamboo shoots", "Rhubarb", "Watercress", "Sorrel", "Collard greens", "Chili flakes",
            "Dandelion greens", "Moringa", "Chives", "Bok choy", "Mustard greens", "Radicchio", "Seaweed", "Tarragon", 
            "Oregano", "Coriander", "Thyme"
        ];
        const fruits = [
            "Apple", "Banana", "Strawberry", "Orange", "Grapes", "Mango", "Pineapple", "Peach", "Plum", "Kiwi", 
            "Cherry", "Blueberry", "Raspberry", "Blackberry", "Papaya", "Watermelon", "Cantaloupe", "Lemon", "Lime", 
            "Grapefruit", "Pear", "Pomegranate", "Fig", "Apricot", "Dragonfruit", "Passionfruit", "Lychee", 
            "Tangerine", "Starfruit", "Guava", "Coconut", "Durian", "Jackfruit", "Persimmon", "Mulberry", "Clementine", 
            "Figs", "Persimmons", "Nectarine", "Soursop", "Blood orange", "Cherimoya", "Acai berry", "Goji berry",
            "Elderberry", "Pineberry", "Tamarillo", "Quince", "Jabuticaba", "Longan", "Salak", "Breadfruit"
        ];
        const veggies = [
            "Corn", "Beets", "Lettuce", "Celery", "Carrot", "Peas", "Potatoes", "Brussels sprouts", "Sweet corn", 
            "Bell pepper", "Tomatoes", "Asparagus", "Cabbage", "Cauliflower", "Cucumber", "Spinach", "Zucchini", 
            "Leeks", "Kale", "Chard", "Radishes", "Arugula", "Rutabaga", "Turnip", "Okra", "Chili pepper", 
            "Fennel", "Onion", "Garlic", "Shallots", "Chives", "Watercress", "Endive", "Bok choy", "Mustard greens",
            "Edamame", "Chayote", "Kohlrabi", "Napa cabbage", "Shiitake mushrooms", "Daikon", "Sunchokes", "Yucca",
            "Mache", "Wheatgrass", "Sweet peas", "Mizuna", "Taro", "Lotus root", "Fiddlehead ferns", "Bamboo shoots", 
            "Chili flakes"
        ];

        // Price for each ingredient (example)
        const pricesPerIngredient = {
            "Beef": 5, "Chicken": 4, "Pork": 3, "Lamb": 6, "Venison": 8, "Rabbit": 7, "Goat": 5, "Duck": 6, 
            "Bison": 7, "Kangaroo": 9, "Turkey": 4, "Boar": 8, "Elk": 10, "Emu": 7, "Ostrich": 8, "Quail": 6, 
            "Pheasant": 6, "Goose": 7, "Sausage": 3, "Pastrami": 5, "Salami": 4, "Pepperoni": 3, "Jerky": 6,
            "Salmon": 7, "Tuna": 6, "Trout": 5, "Cod": 4, "Herring": 3, "Sardine": 2, "Mackerel": 5, "Swordfish": 8,
            "Halibut": 7, "Bass": 5, "Pike": 5, "Catfish": 4, "Perch": 4, "Shark": 10, "Anchovy": 3, "Tilapia": 4, 
            "Eel": 6, "Walleye": 6, "Flounder": 5, "Pollock": 4, "Clams": 5, "Mussels": 4, "Shrimp": 6, "Crab": 7,
            "Lobster": 9, "Scallops": 8, "Oysters": 7, "Octopus": 9, "Squid": 5, "Caviar": 10, "Sea bass": 7, 
            "Barracuda": 8, "Snapper": 7, "Mahi Mahi": 7, "Sea trout": 6, "Chilean sea bass": 10, "Red snapper": 6,
            "Carrot": 1, "Potato": 1, "Spinach": 2, "Tomato": 2, "Broccoli": 3, "Cabbage": 2, "Lettuce": 1, 
            "Cauliflower": 3, "Onion": 1, "Garlic": 2, "Peppers": 3, "Zucchini": 2, "Squash": 2, "Pumpkin": 3, 
            "Eggplant": 2, "Beets": 2, "Asparagus": 4, "Radish": 2, "Artichoke": 5, "Kale": 3, "Brussels sprouts": 5,
            "Chard": 3, "Sweet potato": 2, "Cucumber": 2, "Green beans": 3, "Celery": 1, "Leeks": 3, "Parsnips": 3, 
            "Mushrooms": 4, "Fennel": 3, "Turnips": 2, "Olives": 3, "Chili peppers": 2, "Okra": 4, "Taro root": 5, 
            "Nori": 2, "Algae": 3, "Bamboo shoots": 2, "Rhubarb": 3, "Watercress": 4, "Sorrel": 3, "Collard greens": 3,
            "Chives": 2, "Bok choy": 3, "Mustard greens": 3, "Radicchio": 3, "Seaweed": 3, "Tarragon": 2, "Oregano": 2,
            "Coriander": 2, "Thyme": 2, "Apple": 2, "Banana": 1, "Strawberry": 3, "Orange": 2, "Grapes": 3, "Mango": 4,
            "Pineapple": 3, "Peach": 3, "Plum": 2, "Kiwi": 3, "Cherry": 4, "Blueberry": 3, "Raspberry": 3, 
            "Blackberry": 3, "Papaya": 5, "Watermelon": 3, "Cantaloupe": 3, "Lemon": 2, "Lime": 2, "Grapefruit": 3,
            "Pear": 2, "Pomegranate": 4, "Fig": 4, "Apricot": 3, "Dragonfruit": 6, "Passionfruit": 5, "Lychee": 5,
            "Tangerine": 2, "Starfruit": 4, "Guava": 4, "Coconut": 5, "Durian": 7, "Jackfruit": 6, "Persimmon": 5,
            "Mulberry": 4, "Clementine": 2, "Figs": 4, "Persimmons": 5, "Nectarine": 3, "Soursop": 5, "Blood orange": 3,
            "Cherimoya": 6, "Acai berry": 7, "Goji berry": 4, "Elderberry": 4, "Pineberry": 6, "Tamarillo": 4,
            "Quince": 3, "Jabuticaba": 5, "Longan": 5, "Salak": 5, "Breadfruit": 5
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

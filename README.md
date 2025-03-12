<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Recipe Game</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f1f1f1;
      color: #333;
      margin: 0;
      padding: 20px;
    }
    h1, h2 {
      color: #4CAF50;
    }
    .ingredient-list {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }
    .ingredient-btn {
      margin: 5px;
      padding: 10px;
      background-color: #4CAF50;
      color: white;
      border: none;
      cursor: pointer;
      border-radius: 5px;
    }
    .ingredient-btn:hover {
      background-color: #45a049;
    }
    .dish-info {
      margin-top: 20px;
      background-color: #fff;
      padding: 15px;
      border-radius: 5px;
      box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
    }
    .dish-info h3 {
      margin-bottom: 10px;
      color: #4CAF50;
    }
    .dish-info p {
      margin: 5px 0;
    }
    .calculate-btn {
      background-color: #2196F3;
      color: white;
      padding: 10px 20px;
      border: none;
      cursor: pointer;
      margin-top: 10px;
      border-radius: 5px;
    }
    .calculate-btn:hover {
      background-color: #1976D2;
    }
  </style>
</head>
<body>

  <h1>Recipe Creator Game</h1>

  <div id="ingredient-section">
    <h2>Select Your Ingredients</h2>

    <!-- Vegetables -->
    <div>
      <h3>Vegetables</h3>
      <div class="ingredient-list" id="vegetables">
        <!-- Buttons for vegetables will be inserted here -->
      </div>
    </div>

    <!-- Fruits -->
    <div>
      <h3>Fruits</h3>
      <div class="ingredient-list" id="fruits">
        <!-- Buttons for fruits will be inserted here -->
      </div>
    </div>

    <!-- Proteins -->
    <div>
      <h3>Proteins</h3>
      <div class="ingredient-list" id="proteins">
        <!-- Buttons for proteins will be inserted here -->
      </div>
    </div>

    <!-- Fish -->
    <div>
      <h3>Fish</h3>
      <div class="ingredient-list" id="fish">
        <!-- Buttons for fish will be inserted here -->
      </div>
    </div>

    <!-- More ingredient categories can be added as needed -->
  </div>

  <!-- Dish Information and Calculate Section -->
  <div id="dish-info" class="dish-info">
    <h3>Your Dish</h3>
    <p><strong>Dish Name:</strong> <span id="dish-name">Your Dish</span></p>
    <p><strong>Ingredients:</strong> <span id="ingredients-list">None selected</span></p>
    <p><strong>Price: </strong><span id="dish-price">$0</span></p>
    <p><strong>Dish Rating:</strong> <span id="dish-rating">Not rated</span></p>
    <button class="calculate-btn" id="calculate-btn">Calculate Price</button>
  </div>

  <script>
    // Arrays of ingredients for each category (Vegetables, Fruits, Proteins, Fish, etc.)
    const vegetables = [
      "Tomato", "Cucumber", "Carrot", "Onion", "Bell Pepper", "Lettuce", "Spinach", "Zucchini", "Broccoli", "Cauliflower",
      "Eggplant", "Potato", "Sweet Potato", "Garlic", "Ginger", "Peas", "Green Beans", "Asparagus", "Mushrooms", "Brussels Sprouts",
      "Leek", "Beetroot", "Kale", "Cabbage", "Chard", "Arugula", "Celeriac", "Radish", "Turnip", "Butternut Squash", "Parsnip",
      "Rutabaga", "Pumpkin", "Fennel", "Chili Pepper", "Okra", "Artichoke", "Tomatillo", "Jalapeno", "Snow Peas", "Shallots",
      "Chives", "Sweet Corn", "Fennel", "Chili", "Celery", "Chili Pepper", "Romaine Lettuce", "Cabbage", "Endive", "Bok Choy",
      "Leeks", "Red Cabbage", "Sweet Peas", "Fennel Bulb", "Chicory", "Taro Root", "Daikon Radish", "Zucchini Squash", "Savoy Cabbage",
      "Chayote", "Coriander", "Pumpkin", "Chili", "Cucumber", "Carrot", "Squash", "Snap Peas", "Soybeans", "Swiss Chard", "Garlic Scapes",
      "Chinese Cabbage", "Scallions", "Oregano", "Parsley", "Basil", "Thyme", "Rosemary", "Cilantro", "Mints", "Dandelion Greens",
      "Shitake Mushrooms", "Portobello Mushrooms", "Chanterelle Mushrooms", "Morel Mushrooms", "Tarragon", "Savoy Cabbage", "Purple Cabbage",
      "Baby Corn", "Fennel", "Bamboo Shoots", "Chili Paste", "Miso Paste", "Yam", "Ramps", "Chili Flakes", "Dandelion Greens", "Kohlrabi",
      "Edamame", "Fava Beans", "Soy Milk", "Tofu", "Tempeh"
    ];

    const fruits = [
      "Apple", "Banana", "Orange", "Grapes", "Blueberry", "Pineapple", "Peach", "Strawberry", "Raspberry", "Blackberry",
      "Mango", "Papaya", "Watermelon", "Kiwi", "Lemon", "Lime", "Cantaloupe", "Pear", "Cherry", "Plum", "Pomegranate",
      "Grapefruit", "Fig", "Apricot", "Dragonfruit", "Lychee", "Starfruit", "Passionfruit", "Mulberry", "Tangerine", "Coconut",
      "Date", "Pluot", "Rhubarb", "Goji Berry", "Quince", "Persimmon", "Soursop", "Acai Berry", "Avocado", "Black Currant",
      "Red Currant", "Jackfruit", "Nectarine", "Custard Apple", "Loquat", "Guanabana", "Longan", "Salak", "Clementine", "Soursop",
      "Jaboticaba", "Cape Gooseberry", "Durian", "Mangosteen", "Baobab", "Yunnan Hackberry", "Surinam Cherry", "Limequat",
      "Pomelo", "Carambola", "Jelly Palm", "Tamarillo", "Blood Orange", "Pomelo", "Mango Papaya", "Strawberry Guava", "Golden Kiwi",
      "Soursop", "Kumquat", "Black Grapes", "Green Apple", "Red Dragonfruit", "Green Dragonfruit", "Pink Guava", "Fuyu Persimmon",
      "Pineberry", "Pink Grapefruit", "Golden Pear", "Cranberry", "Indian Gooseberry", "Sea Buckthorn", "Tamarind", "Salsify", "Lingonberry",
      "Blueberry Peach", "Pineapple Guava", "Raspberry Lemon", "Blueberry Jam", "Lychee Rose", "Pomelo Lime", "Passionfruit Strawberry",
      "Watermelon Mint", "Tangerine Blossom", "Mandarins", "Maracuja", "Blood Orange", "Watermelon Peach", "Mango Lime", "Tropical Citrus"
    ];

    const proteins = [
      "Chicken", "Beef", "Pork", "Lamb", "Turkey", "Duck", "Salmon", "Tuna", "Cod", "Shrimp", "Crab", "Lobster", "Swordfish",
      "Herring", "Trout", "Mackerel", "Halibut", "Octopus", "Squid", "Tofu", "Tempeh", "Seitan", "Egg", "Chickpeas", "Lentils",
      "Black Beans", "Kidney Beans", "Edamame", "Peas", "Quinoa", "Paneer", "Chicken Sausage", "Beef Sausage", "Pork Sausage",
      "Salmon Fillet", "Chicken Thigh", "Chicken Breast", "Steak", "Pork Chop", "Lamb Chops", "Lobster Tail", "Crab Legs", "Chicken Wings",
      "Venison", "Rabbit", "Goat", "Bison", "Quail", "Sardines", "Anchovies", "Egg Whites", "Almonds", "Pistachios", "Cashews",
      "Peanut Butter", "Sunflower Seeds", "Pumpkin Seeds", "Chia Seeds", "Hemp Seeds", "Flax Seeds", "Coconut Flakes", "Coconut Milk",
      "Mushrooms", "Ghee", "Butter", "Cottage Cheese", "Greek Yogurt", "Cheddar Cheese", "Parmesan", "Mozzarella", "Ricotta", "Feta",
      "Brie", "Cream Cheese", "Goat Cheese", "Vegan Cheese", "Ricotta", "Eggplant", "Tempeh", "Vegan Sausage", "Chickpea Patties",
      "Vegan Tacos", "Soy Milk", "Seitan", "Sausage", "Vegan Meatballs", "Tofu Skewers", "Vegan Stew", "Vegan Ribs", "Jackfruit Ribs",
      "Vegan Bacon", "Coconut Yogurt", "Vegan Butter", "Silken Tofu", "Textured Vegetable Protein"
    ];

    const fish = [
      "Salmon", "Tuna", "Cod", "Herring", "Mackerel", "Trout", "Sardines", "Anchovies", "Halibut", "Swordfish", "Tilapia",
      "Yellowtail", "Pollock", "Clams", "Mussels", "Oysters", "Crab", "Lobster", "Shrimp", "Scallops", "Octopus", "Squid", "Eel",
      "Flounder", "Sea Bass", "Snapper", "Sturgeon", "Bluefish", "Gudgeon", "Pike", "Perch", "Barracuda", "Wahoo", "Pomfret",
      "Grouper", "Tilapia", "Bass", "Carp", "Catfish", "Angelfish", "Trout", "Bluegill", "Redfish", "Rainbow Trout", "Rockfish",
      "Sunfish", "Kingfish", "Yellowfin Tuna", "Whitefish", "Butterfish", "Black Bass", "Wreckfish", "Swai", "Largemouth Bass", "Sole",
      "Gurnard", "Bream", "Mahi-Mahi", "Zander", "Porgy", "Butterfish", "Tilefish", "Tautog", "Cobia", "Sea Cucumber", "Amberjack",
      "Jellyfish", "Lobster Tail", "Catfish Fillet", "Tilapia Fillet", "Swordfish Steaks", "Grilled Salmon", "Freshwater Fish",
      "Shrimp Cocktail", "King Crab", "Grilled Lobster", "Baked Cod", "Baked Trout", "Poached Salmon", "Fish Tacos", "Tuna Tartare",
      "Mussels in White Wine", "Baked Halibut", "Fried Clams", "Grilled Fish", "Fried Shrimp", "Fish Stew", "Grilled Mahi-Mahi",
      "Poached Cod", "Seared Scallops", "Clam Chowder", "Fish Cakes", "Shrimp Scampi", "Mussels with Garlic", "Fish Soup", "Seafood Paella"
    ];

    // Function to display ingredient buttons
    function displayIngredients() {
      const categories = [
        { name: "vegetables", data: vegetables },
        { name: "fruits", data: fruits },
        { name: "proteins", data: proteins },
        { name: "fish", data: fish }
      ];

      categories.forEach(category => {
        const container = document.getElementById(category.name);
        category.data.forEach(ingredient => {
          const btn = document.createElement("button");
          btn.classList.add("ingredient-btn");
          btn.textContent = ingredient;
          btn.onclick = () => addIngredientToDish(ingredient);
          container.appendChild(btn);
        });
      });
    }

    // Dish and ingredient handling
    let selectedIngredients = [];
    let dishPrice = 0;

    function addIngredientToDish(ingredient) {
      if (!selectedIngredients.includes(ingredient)) {
        selectedIngredients.push(ingredient);
        updateDishInfo();
      }
    }

    // Update the dish info dynamically
    function updateDishInfo() {
      const dishName = "Dish of the Day";
      const dishRating = "4.5";  // This can be dynamic based on your preference
      const ingredientsList = selectedIngredients.join(", ");
      const price = selectedIngredients.length * 5;  // Just an example: $5 per ingredient

      document.getElementById("dish-name").textContent = dishName;
      document.getElementById("ingredients-list").textContent = ingredientsList;
      document.getElementById("dish-price").textContent = `$${price}`;
      document.getElementById("dish-rating").textContent = dishRating;
    }

    // Initialize ingredients and display them
    displayIngredients();

    // Handle the calculation (e.g., after dish creation)
    document.getElementById("calculate-btn").onclick = () => {
      alert("Price has been calculated based on selected ingredients!");
    };
  </script>
</body>
</html>

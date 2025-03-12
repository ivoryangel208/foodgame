<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dish Creation Game</title>
  <style>
    body {
      font-family: 'Roboto', sans-serif;
      background: linear-gradient(to right, #e0f7fa, #ffffff);
      color: #333;
      margin: 0;
      padding: 0;
    }

    .container {
      padding: 20px;
    }

    h1 {
      text-align: center;
      font-size: 40px;
      color: #2c3e50;
    }

    .ingredient-container {
      margin-top: 20px;
    }

    .ingredient-tab {
      background-color: #ff6347;
      color: white;
      padding: 15px;
      margin: 5px 0;
      border-radius: 12px;
      border: none;
      cursor: pointer;
      font-size: 18px;
      width: 100%;
      text-align: left;
    }

    .ingredient-tab:hover {
      background-color: #ff4500;
    }

    .ingredient-list {
      display: none;
      padding-left: 20px;
      margin-top: 10px;
    }

    .ingredient-btn {
      background-color: #fff;
      color: #333;
      padding: 10px;
      margin: 5px;
      border-radius: 8px;
      border: 1px solid #ccc;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    .ingredient-btn:hover {
      background-color: #f1f1f1;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
    }

    .dish-info {
      background-color: #f9f9f9;
      border-radius: 15px;
      padding: 20px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      margin-top: 20px;
    }

    .dish-info h2 {
      font-size: 24px;
      font-weight: bold;
      color: #333;
    }

    .dish-info p {
      font-size: 18px;
      color: #666;
    }

    .dish-price {
      font-size: 24px;
      font-weight: bold;
      color: #ff6347;
    }

    .footer {
      position: fixed;
      bottom: 0;
      left: 0;
      width: 100%;
      background-color: #333;
      color: white;
      text-align: center;
      padding: 10px 0;
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>Create Your Dish</h1>

    <div class="ingredient-container" id="ingredient-container">
      <!-- Dynamically Generated Ingredient Tabs -->
    </div>

    <div class="dish-info">
      <h2>Dish Name: <span id="dish-name">No Dish Created</span></h2>
      <p>Ingredients: <span id="ingredients-list">None</span></p>
      <p>Price: <span id="dish-price">$0</span></p>
      <p>Rating: <span id="dish-rating">0</span> ★</p>
    </div>

    <div class="footer">
      <button onclick="createDish()">Create Dish</button>
    </div>
  </div>

  <script>
    // Generate a set of 200 unique ingredients for each type (Meat, Fish, Vegetables, etc.)
    function generateIngredients() {
      const types = ['Meat', 'Fish', 'Vegetable', 'Fruit', 'Grain'];
      const allIngredients = [];

      types.forEach(type => {
        for (let i = 1; i <= 200; i++) {
          allIngredients.push({
            name: `${type} Ingredient ${i}`,
            price: (Math.random() * 10 + 1).toFixed(2),
            type: type
          });
        }
      });

      return allIngredients;
    }

    // List of 1000 ingredients (200 for each type)
    const ingredients = generateIngredients();

    // Group ingredients by type
    const groupedIngredients = ingredients.reduce((groups, ingredient) => {
      if (!groups[ingredient.type]) {
        groups[ingredient.type] = [];
      }
      groups[ingredient.type].push(ingredient);
      return groups;
    }, {});

    // Dynamically create ingredient tabs
    const ingredientContainer = document.getElementById('ingredient-container');
    Object.keys(groupedIngredients).forEach(type => {
      const tabButton = document.createElement('button');
      tabButton.className = 'ingredient-tab';
      tabButton.textContent = `${type} Ingredients`;
      tabButton.onclick = () => toggleIngredientList(type);
      ingredientContainer.appendChild(tabButton);

      const ingredientList = document.createElement('div');
      ingredientList.className = 'ingredient-list';
      groupedIngredients[type].forEach(ingredient => {
        const button = document.createElement('button');
        button.className = 'ingredient-btn';
        button.textContent = ingredient.name;
        button.onclick = () => addIngredient(ingredient);
        ingredientList.appendChild(button);
      });

      ingredientContainer.appendChild(ingredientList);
    });

    let selectedIngredients = [];
    let dishName = '';

    // Toggle ingredient list visibility
    function toggleIngredientList(type) {
      const list = document.querySelectorAll(`.ingredient-list`);
      list.forEach(listElement => {
        if (listElement.previousSibling.textContent === `${type} Ingredients`) {
          listElement.style.display = listElement.style.display === 'block' ? 'none' : 'block';
        } else {
          listElement.style.display = 'none';
        }
      });
    }

    // Add ingredient to the dish
    function addIngredient(ingredient) {
      if (!selectedIngredients.includes(ingredient)) {
        selectedIngredients.push(ingredient);
        updateDishInfo();
      }
    }

    // Update the displayed dish information
    function updateDishInfo() {
      const ingredientNames = selectedIngredients.map(ingredient => ingredient.name).join(', ');
      const price = selectedIngredients.reduce((total, ingredient) => total + parseFloat(ingredient.price), 0);
      const rating = (Math.random() * 5).toFixed(1);

      document.getElementById('ingredients-list').textContent = ingredientNames || 'None';
      document.getElementById('dish-price').textContent = `$${price.toFixed(2)}`;
      document.getElementById('dish-rating').textContent = rating;
    }

    // Generate a random name for the dish
    function generateDishName() {
      const dishNames = ['Tasty Treat', 'Gourmet Delight', 'Savory Feast', 'Exotic Platter'];
      return dishNames[Math.floor(Math.random() * dishNames.length)];
    }

    // Create the dish
    function createDish() {
      dishName = generateDishName();
      document.getElementById('dish-name').textContent = dishName;
      selectedIngredients = [];
      updateDishInfo();
    }
  </script>

</body>
</html>

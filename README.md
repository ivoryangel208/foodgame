<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Farm-to-Table Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            text-align: center;
        }
        h1 {
            font-size: 2.5rem;
            color: #2e7d32;
        }
        p {
            font-size: 1.2rem;
            color: #333;
        }
        button {
            background-color: #388e3c;
            color: white;
            font-size: 1.2rem;
            padding: 10px 20px;
            margin: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #4caf50;
        }
        .emoji {
            font-size: 3rem;
            margin: 15px;
        }
        #result {
            font-size: 1.5rem;
            color: #333;
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <h1>Farm-to-Table Game</h1>
    <p>Choose a food item, then a cooking action, and finally a utensil to serve it!</p>

    <div id="food-buttons">
        <button onclick="selectFood('🍅 Tomatoes')">🍅 Tomatoes</button>
        <button onclick="selectFood('🥕 Carrots')">🥕 Carrots</button>
        <button onclick="selectFood('🌽 Corn')">🌽 Corn</button>
        <button onclick="selectFood('🥔 Potatoes')">🥔 Potatoes</button>
    </div>

    <div id="action-buttons" style="display: none;">
        <p>How do you want to cook the food?</p>
        <button onclick="selectAction('Grill')">Grill</button>
        <button onclick="selectAction('Boil')">Boil</button>
        <button onclick="selectAction('Fry')">Fry</button>
        <button onclick="selectAction('Steam')">Steam</button>
    </div>

    <div id="utensil-buttons" style="display: none;">
        <p>How do you want to serve it?</p>
        <button onclick="selectUtensil('Plate')">Plate</button>
        <button onclick="selectUtensil('Bowl')">Bowl</button>
        <button onclick="selectUtensil('Cup')">Cup</button>
    </div>

    <div id="result"></div>

    <script>
        let selectedFood = '';
        let selectedAction = '';
        let selectedUtensil = '';

        // Select food item
        function selectFood(food) {
            selectedFood = food;
            document.getElementById('food-buttons').style.display = 'none';
            document.getElementById('action-buttons').style.display = 'block';
            document.getElementById('result').textContent = `You selected ${food}. Now, how do you want to cook it?`;
        }

        // Select cooking action
        function selectAction(action) {
            if (!selectedFood) {
                document.getElementById('result').textContent = 'Please select a food item first!';
                return;
            }
            selectedAction = action;
            document.getElementById('action-buttons').style.display = 'none';
            document.getElementById('utensil-buttons').style.display = 'block';
            document.getElementById('result').textContent = `You decided to ${action} the ${selectedFood}. Now, how do you want to serve it?`;
        }

        // Select serving utensil
        function selectUtensil(utensil) {
            if (!selectedAction) {
                document.getElementById('result').textContent = 'Please choose a cooking action first!';
                return;
            }
            selectedUtensil = utensil;
            document.getElementById('utensil-buttons').style.display = 'none';
            document.getElementById('result').textContent = `You served the ${selectedFood} on a ${utensil} after ${selectedAction}. Enjoy!`;
        }
    </script>

</body>
</html>


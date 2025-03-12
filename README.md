<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Farm-to-Table Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f8ff;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            flex-direction: column;
        }
        h1 {
            text-align: center;
            font-size: 2.5rem;
            margin-bottom: 20px;
            color: #4caf50;
        }
        button {
            background-color: #4caf50;
            color: white;
            font-size: 1.2rem;
            padding: 15px;
            margin: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #45a049;
        }
        .emoji {
            font-size: 2.5rem;
            margin: 20px;
        }
        .result {
            font-size: 1.5rem;
            color: #333;
            text-align: center;
            margin-top: 20px;
        }
        .game-container {
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>Farm-to-Table Game</h1>
        <p>Choose a food item to cook and serve!</p>
        
        <div class="emoji">
            <button onclick="makeDish('🍅 Tomatoes')">🍅 Tomatoes</button>
            <button onclick="makeDish('🥕 Carrots')">🥕 Carrots</button>
            <button onclick="makeDish('🌽 Corn')">🌽 Corn</button>
            <button onclick="makeDish('🥔 Potatoes')">🥔 Potatoes</button>
        </div>
        
        <p>Choose how you want to cook the food!</p>
        
        <div class="emoji">
            <button onclick="actionChoice('Grill')">Grill</button>
            <button onclick="actionChoice('Boil')">Boil</button>
            <button onclick="actionChoice('Fry')">Fry</button>
            <button onclick="actionChoice('Steam')">Steam</button>
        </div>

        <p>Choose a utensil to serve the food!</p>
        
        <div class="emoji">
            <button onclick="utensilChoice('Plate')">Plate</button>
            <button onclick="utensilChoice('Bowl')">Bowl</button>
            <button onclick="utensilChoice('Cup')">Cup</button>
        </div>

        <div class="result" id="result"></div>
    </div>

    <script>
        let selectedFood = '';
        let selectedAction = '';
        let selectedUtensil = '';
        
        function makeDish(food) {
            selectedFood = food;
            document.getElementById('result').textContent = `You selected ${food}! Let's cook it!`;
        }

        function actionChoice(action) {
            if (!selectedFood) {
                document.getElementById('result').textContent = 'Please select a food item first!';
                return;
            }
            selectedAction = action;
            document.getElementById('result').textContent = `You decided to ${action} the ${selectedFood}!`;
        }

        function utensilChoice(utensil) {
            if (!selectedAction) {
                document.getElementById('result').textContent = 'Please choose a cooking action first!';
                return;
            }
            selectedUtensil = utensil;
            document.getElementById('result').textContent = `You served the ${selectedFood} on a ${utensil} after ${selectedAction}.`;
        }
    </script>
</body>
</html>

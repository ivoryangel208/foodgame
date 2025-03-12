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
        
        <div class="result" id="result"></div>
    </div>

    <script>
        function makeDish(food) {
            const result = document.getElementById('result');
            let resultText = '';

            switch(food) {
                case '🍅 Tomatoes':
                    resultText = 'You selected Tomatoes! 🍅 A healthy start!';
                    break;
                case '🥕 Carrots':
                    resultText = 'You selected Carrots! 🥕 Packed with vitamins!';
                    break;
                case '🌽 Corn':
                    resultText = 'You selected Corn! 🌽 A tasty and filling choice!';
                    break;
                case '🥔 Potatoes':
                    resultText = 'You selected Potatoes! 🥔 Comfort food at its finest!';
                    break;
                default:
                    resultText = 'Please select a food item.';
            }

            result.textContent = resultText;
        }
    </script>
</body>
</html>


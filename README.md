<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Lost Recipe</title>
    <style>
        body { 
            text-align: center; 
            font-family: 'Poppins', sans-serif; 
            background: linear-gradient(to right, #ffefd5, #f8c471); 
            padding: 20px;
        }
        #gameArea { 
            margin-top: 20px; 
            display: flex; 
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
        }
        .ingredient { 
            font-size: 50px; 
            cursor: grab; 
            display: inline-block; 
            padding: 20px; 
            background: white; 
            border-radius: 50%; 
            box-shadow: 4px 4px 15px rgba(0,0,0,0.3);
            transition: transform 0.2s;
        }
        .ingredient:hover {
            transform: scale(1.1);
        }
        #pot { 
            width: 180px; 
            height: 180px; 
            border-radius: 50%; 
            background: #d2691e; 
            color: white; 
            font-size: 50px; 
            display: flex; 
            align-items: center; 
            justify-content: center; 
            box-shadow: 4px 4px 15px rgba(0,0,0,0.3);
            margin: 30px auto; 
            transition: background 0.3s, transform 0.2s;
        }
        #pot.success { background: #32cd32; transform: scale(1.1); }
        #pot.fail { background: #ff4500; transform: scale(0.9); }
        p#message {
            font-size: 22px;
            font-weight: bold;
            margin-top: 15px;
            color: #333;
        }
        #hintButton {
            padding: 10px 20px;
            font-size: 18px;
            background: #3498db;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 15px;
        }
        #hintButton:hover {
            background: #2980b9;
        }
    </style>
</head>
<body>
    <h1>The Lost Recipe 🍽️</h1>
    <p>Drag the correct ingredients into the pot! 🍲</p>
    <button id="hintButton" onclick="showHint()">Hint 🔍</button>
    <p id="hint"></p>
    <div id="gameArea"></div>
    <div id="pot" ondrop="drop(event)" ondragover="allowDrop(event)">🍲</div>
    <p id="message"></p>
    
    <script>
        const recipes = [
            { name: "Vegetable Soup", ingredients: ["🥕", "🍅", "🧅"] },
            { name: "Fruit Salad", ingredients: ["🍎", "🍌", "🍊"] },
            { name: "Spaghetti", ingredients: ["🍅", "🧄", "🍝"] },
            { name: "Omelette", ingredients: ["🥚", "🧀", "🧅"] },
            { name: "Taco", ingredients: ["🌮", "🥩", "🧀"] }
        ];
        
        let selectedRecipe = recipes[Math.floor(Math.random() * recipes.length)];
        let correctIngredients = selectedRecipe.ingredients;
        let chosenIngredients = [];
        
        function loadIngredients() {
            let gameArea = document.getElementById("gameArea");
            gameArea.innerHTML = "";
            let allIngredients = ["🥕", "🍅", "🧅", "🍎", "🍌", "🍊", "🧄", "🍝", "🥚", "🧀", "🌮", "🥩", "🌶️", "🥦", "🍞", "🧂"];
            
            allIngredients.sort(() => 0.5 - Math.random());
            allIngredients.slice(0, 8).forEach(ingredient => {
                let div = document.createElement("div");
                div.classList.add("ingredient");
                div.draggable = true;
                div.ondragstart = drag;
                div.innerText = ingredient;
                gameArea.appendChild(div);
            });
        }
        
        function allowDrop(event) {
            event.preventDefault();
        }
        function drag(event) {
            event.dataTransfer.setData("text", event.target.innerText);
        }
        function drop(event) {
            event.preventDefault();
            let data = event.dataTransfer.getData("text");
            let pot = document.getElementById("pot");
            let message = document.getElementById("message");
            
            if (!chosenIngredients.includes(data)) {
                chosenIngredients.push(data);
                pot.innerText += data;
            }
            
            if (chosenIngredients.length >= 3) {
                if (correctIngredients.every(ing => chosenIngredients.includes(ing))) {
                    pot.classList.add("success");
                    message.innerText = `You made ${selectedRecipe.name}! ✅`;
                } else {
                    pot.classList.add("fail");
                    message.innerText = "Wrong ingredients! ❌ Try again.";
                }
                setTimeout(() => {
                    pot.classList.remove("success", "fail");
                    resetGame();
                }, 1000);
            }
        }
        
        function showHint() {
            document.getElementById("hint").innerText = `Hint: Think about what goes into ${selectedRecipe.name}.`;
        }
        
        function resetGame() {
            selectedRecipe = recipes[Math.floor(Math.random() * recipes.length)];
            correctIngredients = selectedRecipe.ingredients;
            chosenIngredients = [];
            document.getElementById("pot").innerText = "🍲";
            document.getElementById("message").innerText = "";
            document.getElementById("hint").innerText = "";
            loadIngredients();
        }
        
        loadIngredients();
    </script>
</body>
</html>

# Cat-Calculator-App
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meow Calculator</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="paw-print">🐾</div>
    <div class="paw-print">🐾</div>
    <div class="paw-print">🐾</div>
    <div class="paw-print">🐾</div>
    
    <div class="calculator">
        <div class="whiskers"></div>
        
        <div class="cat-header">
            <div class="cat-face">😸</div>
            <h1 class="cat-title">Meow Calculator</h1>
        </div>
        
        <input type="text" class="display" id="display" readonly placeholder="0">
        
        <div class="buttons">
            <button class="btn btn-special" onclick="clearDisplay()">C</button>
            <button class="btn btn-special" onclick="deleteLast()">⌫</button>
            <button class="btn btn-operator" onclick="appendToDisplay('/')">/</button>
            <button class="btn btn-operator" onclick="appendToDisplay('*')">×</button>
            
            <button class="btn btn-number" onclick="appendToDisplay('7')">7</button>
            <button class="btn btn-number" onclick="appendToDisplay('8')">8</button>
            <button class="btn btn-number" onclick="appendToDisplay('9')">9</button>
            <button class="btn btn-operator" onclick="appendToDisplay('-')">-</button>
            
            <button class="btn btn-number" onclick="appendToDisplay('4')">4</button>
            <button class="btn btn-number" onclick="appendToDisplay('5')">5</button>
            <button class="btn btn-number" onclick="appendToDisplay('6')">6</button>
            <button class="btn btn-operator" onclick="appendToDisplay('+')">+</button>
            
            <button class="btn btn-number" onclick="appendToDisplay('1')">1</button>
            <button class="btn btn-number" onclick="appendToDisplay('2')">2</button>
            <button class="btn btn-number" onclick="appendToDisplay('3')">3</button>
            <button class="btn btn-number" onclick="appendToDisplay('0')" style="grid-row: span 2; height: 135px; border-radius: 30px;">0</button>
            
            <button class="btn btn-equals" onclick="calculate()">=</button>
            <button class="btn btn-number" onclick="appendToDisplay('.')">.</button>
        </div>
        
        <div class="error-message" id="errorMessage"></div>
    </div>

    <script src="script.js"></script>
</body>
</html>

Cat Calculator
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meow Calculator</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Fredoka+One:wght@400&family=Nunito:wght@600;700&display=swap');
        
        body {
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #fecfef 100%);
            min-height: 100vh;
            font-family: 'Nunito', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
            overflow-x: hidden;
        }
        
        /* Floating paw prints background */
        .paw-print {
            position: fixed;
            opacity: 0.1;
            font-size: 2rem;
            color: #ff6b9d;
            animation: float 8s ease-in-out infinite;
            z-index: 0;
        }
        
        .paw-print:nth-child(1) { top: 10%; left: 10%; animation-delay: 0s; }
        .paw-print:nth-child(2) { top: 20%; right: 15%; animation-delay: 2s; }
        .paw-print:nth-child(3) { bottom: 20%; left: 20%; animation-delay: 4s; }
        .paw-print:nth-child(4) { bottom: 10%; right: 10%; animation-delay: 6s; }
        
        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(5deg); }
        }
        
        .calculator {
            background: #fff;
            border-radius: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            padding: 30px;
            max-width: 350px;
            width: 100%;
            position: relative;
            z-index: 1;
            border: 5px solid #ff6b9d;
        }
        
        .cat-header {
            text-align: center;
            margin-bottom: 25px;
            position: relative;
        }
        
        .cat-face {
            font-size: 4rem;
            margin-bottom: 10px;
            animation: blink 3s infinite;
        }
        
        @keyframes blink {
            0%, 95% { content: '😸'; }
            96%, 100% { content: '😹'; }
        }
        
        .cat-title {
            font-family: 'Fredoka One', cursive;
            font-size: 2rem;
            color: #ff6b9d;
            margin: 0;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }
        
        .display {
            background: linear-gradient(45deg, #667eea 0%, #764ba2 100%);
            border: none;
            border-radius: 20px;
            color: white;
            font-size: 2rem;
            font-weight: 700;
            padding: 20px;
            text-align: right;
            width: 100%;
            margin-bottom: 20px;
            box-shadow: inset 0 5px 10px rgba(0,0,0,0.2);
            font-family: 'Nunito', sans-serif;
        }
        
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px;
        }
        
        .btn {
            border: none;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            font-size: 1.3rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: 'Nunito', sans-serif;
            position: relative;
            overflow: hidden;
        }
        
        .btn:hover {
            transform: scale(1.1);
            box-shadow: 0 8px 20px rgba(0,0,0,0.2);
        }
        
        .btn:active {
            transform: scale(0.95);
        }
        
        .btn-number {
            background: linear-gradient(45deg, #ff9a9e 0%, #fecfef 100%);
            color: #333;
            border: 3px solid #ff6b9d;
        }
        
        .btn-operator {
            background: linear-gradient(45deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: 3px solid #5a6fd8;
        }
        
        .btn-special {
            background: linear-gradient(45deg, #ffecd2 0%, #fcb69f 100%);
            color: #333;
            border: 3px solid #fc9f7f;
        }
        
        .btn-equals {
            background: linear-gradient(45deg, #a8edea 0%, #fed6e3 100%);
            color: #333;
            border: 3px solid #7dd3fc;
            grid-column: span 2;
            border-radius: 30px;
            width: auto;
        }
        
        .btn::after {
            content: '🐾';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 0.8rem;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .btn:hover::after {
            opacity: 0.3;
        }
        
        .whiskers {
            position: absolute;
            top: 20px;
            left: -10px;
            right: -10px;
            height: 2px;
            background: repeating-linear-gradient(
                90deg,
                transparent,
                transparent 10px,
                #ff6b9d 10px,
                #ff6b9d 20px,
                transparent 20px,
                transparent 30px
            );
            opacity: 0.3;
        }
        
        .error-message {
            color: #ff6b9d;
            text-align: center;
            margin-top: 10px;
            font-weight: 600;
            min-height: 20px;
        }
    </style>
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

    <script>
        let currentInput = '';
        let operator = '';
        let previousInput = '';
        let justCalculated = false;
        
        const display = document.getElementById('display');
        const errorMessage = document.getElementById('errorMessage');
        
        function updateDisplay() {
            display.value = currentInput || '0';
        }
        
        function clearDisplay() {
            currentInput = '';
            operator = '';
            previousInput = '';
            justCalculated = false;
            errorMessage.textContent = '';
            updateDisplay();
            
            // Fun cat reaction
            const catFace = document.querySelector('.cat-face');
            catFace.textContent = '😽';
            setTimeout(() => {
                catFace.textContent = '😸';
            }, 500);
        }
        
        function deleteLast() {
            if (currentInput) {
                currentInput = currentInput.slice(0, -1);
                updateDisplay();
            }
        }
        
        function appendToDisplay(value) {
            errorMessage.textContent = '';
            
            if (justCalculated && !isNaN(value)) {
                currentInput = '';
                justCalculated = false;
            }
            
            if (['+', '-', '*', '/'].includes(value)) {
                if (currentInput === '') {
                    if (value === '-') {
                        currentInput = '-';
                    }
                    return;
                }
                
                if (previousInput !== '' && operator !== '' && currentInput !== '') {
                    calculate();
                }
                
                operator = value;
                previousInput = currentInput;
                currentInput = '';
                return;
            }
            
            if (value === '.' && currentInput.includes('.')) {
                return;
            }
            
            currentInput += value;
            updateDisplay();
        }
        
        function calculate() {
            if (previousInput === '' || operator === '' || currentInput === '') {
                return;
            }
            
            const prev = parseFloat(previousInput);
            const current = parseFloat(currentInput);
            let result;
            
            try {
                switch (operator) {
                    case '+':
                        result = prev + current;
                        break;
                    case '-':
                        result = prev - current;
                        break;
                    case '*':
                        result = prev * current;
                        break;
                    case '/':
                        if (current === 0) {
                            throw new Error('Cannot divide by zero! 🙀');
                        }
                        result = prev / current;
                        break;
                    default:
                        return;
                }
                
                // Round to avoid floating point errors
                result = Math.round(result * 100000000) / 100000000;
                
                currentInput = result.toString();
                operator = '';
                previousInput = '';
                justCalculated = true;
                updateDisplay();
                
                // Fun cat reaction for successful calculation
                const catFace = document.querySelector('.cat-face');
                catFace.textContent = '😻';
                setTimeout(() => {
                    catFace.textContent = '😸';
                }, 1000);
                
            } catch (error) {
                errorMessage.textContent = error.message;
                const catFace = document.querySelector('.cat-face');
                catFace.textContent = '🙀';
                setTimeout(() => {
                    catFace.textContent = '😸';
                }, 2000);
            }
        }
        
        // Keyboard support
        document.addEventListener('keydown', function(event) {
            const key = event.key;
            
            if (key >= '0' && key <= '9') {
                appendToDisplay(key);
            } else if (key === '.') {
                appendToDisplay('.');
            } else if (key === '+' || key === '-') {
                appendToDisplay(key);
            } else if (key === '*') {
                appendToDisplay('*');
            } else if (key === '/') {
                event.preventDefault();
                appendToDisplay('/');
            } else if (key === 'Enter' || key === '=') {
                event.preventDefault();
                calculate();
            } else if (key === 'Escape' || key === 'c' || key === 'C') {
                clearDisplay();
            } else if (key === 'Backspace') {
                deleteLast();
            }
        });
        
        // Initialize display
        updateDisplay();
    </script>
</body>
</html>


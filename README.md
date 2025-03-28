<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interface Futurista</title>
    <style>
        body {
            background: #1a1a1a;
            display: flex;
            flex-direction: column;
            align-items: center;
            font-family: 'Arial', sans-serif;
            padding: 20px;
            margin: 0;
            min-height: 100vh;
        }

        .container {
            width: 100%;
            max-width: 400px;
            padding: 20px;
        }

        .turn-section {
            display: flex;
            align-items: center;
            gap: 20px;
            margin-bottom: 40px;
        }

        .btn-turn {
            padding: 15px 25px;
            font-size: 18px;
            background: #00b7ff;
            border: none;
            color: white;
            border-radius: 10px;
            cursor: pointer;
            box-shadow: 0 0 10px #00b7ff;
            transition: all 0.3s;
        }

        .btn-turn:hover {
            box-shadow: 0 0 20px #00b7ff;
        }

        .circles {
            display: flex;
            gap: 15px;
        }

        .circle {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: #555;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 0 5px rgba(255,255,255,0.1);
        }

        .circle.on {
            background: #ff3333;
            box-shadow: 0 0 15px #ff3333;
        }

        .calculator {
            background: #2a2a2a;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(0,183,255,0.2);
        }

        #display {
            width: 100%;
            height: 60px;
            background: #111;
            color: #00ffcc;
            font-size: 28px;
            text-align: right;
            padding: 10px;
            border: none;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: inset 0 0 10px rgba(0,255,204,0.1);
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        button {
            padding: 20px;
            font-size: 20px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            background: #444;
            color: white;
            transition: all 0.3s;
            box-shadow: 0 0 5px rgba(255,255,255,0.1);
        }

        button:hover {
            background: #666;
            box-shadow: 0 0 10px rgba(255,255,255,0.2);
        }

        .op {
            background: #00b7ff;
        }

        .history {
            margin-top: 20px;
            color: #00ffcc;
            font-size: 18px;
        }

        .separator {
            width: 100%;
            height: 2px;
            background: #00b7ff;
            margin: 20px 0;
            box-shadow: 0 0 10px #00b7ff;
        }

        .rules-section {
            color: #00ffcc;
            font-size: 16px;
            text-align: left;
        }

        .rules-section h2 {
            text-align: center;
            color: #00b7ff;
            text-shadow: 0 0 10px #00b7ff;
            margin-bottom: 15px;
        }

        .rules-section p {
            margin: 5px 0;
        }

        .blink {
            animation: blink 0.5s infinite;
        }

        @keyframes blink {
            50% { background: #ff3333; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="turn-section">
            <button class="btn-turn" onclick="nextTurn()">MEU TURNO</button>
            <div class="circles">
                <div class="circle on" onclick="toggleCircle(this)"></div>
                <div class="circle on" onclick="toggleCircle(this)"></div>
                <div class="circle on" onclick="toggleCircle(this)"></div>
                <div class="circle" onclick="toggleCircle(this)"></div>
                <div class="circle" onclick="toggleCircle(this)"></div>
            </div>
        </div>

        <div class="calculator">
            <input type="text" id="display" value="10000" readonly>
            <div class="buttons">
                <button onclick="clearDisplay()">C</button>
                <button onclick="back()">↶</button>
                <button class="op" onclick="operation('-')">-</button>
                <button class="op" onclick="operation('+')">+</button>
                <button onclick="addNumber('7')">7</button>
                <button onclick="addNumber('8')">8</button>
                <button onclick="addNumber('9')">9</button>
                <button onclick="addNumber('4')">4</button>
                <button onclick="addNumber('5')">5</button>
                <button onclick="addNumber('6')">6</button>
                <button onclick="addNumber('1')">1</button>
                <button onclick="addNumber('2')">2</button>
                <button onclick="addNumber('3')">3</button>
                <button onclick="addNumber('0')">0</button>
                <button onclick="calculate()">=</button>
            </div>
        </div>
        <div class="history">Histórico: <span id="history">10000</span></div>
        <div class="separator"></div>
        <div class="rules-section">
            <h2>PAINEL COSMIC DUEL</h2>
            <p><strong>Regras Básicas do Jogo:</strong></p>
            <p><strong>Vida inicial:</strong> 10.000 pontos por jogador.</p>
            <p><strong>Deck:</strong> 36 cartas (monstros, mágicas, armadilhas e campo).</p>
            <p><strong>Energia Cósmica (Esferas vermelhas) 🔴</strong><br>
            Começa com 3 energia, ganha 1 por turno (máximo 5).<br>
            Usada para invocar monstros de nível 3+ e ativar certas cartas.</p>
            <p><strong>Fases do turno:</strong><br>
            • <strong>Compra:</strong> Compre 1 carta.<br>
            • <strong>Principal:</strong> Invoque monstros, use mágicas/armadilhas.<br>
            (Um monstro por turno a não ser que um efeito permita mais monstros serem invocados, cartas mágicas/armadilhas sem limite de invocação).<br>
            • <strong>Batalha:</strong> Ataque com monstros.<br>
            • <strong>Final:</strong> Ajuste o campo e passe o turno.</p>
            <p><strong>Invocação:</strong><br>
            Níveis 1-4: Sem sacrifício (3-4 custam Energia).<br>
            Níveis 5-6: Sacrifique 1 monstro + Energia.<br>
            Nível 7 (raro): Sacrifique 2 monstros + Energia.</p>
            <p><strong>Combate:</strong><br>
            Ataque direto ou contra monstros; Atacar em DEF não tira dano, mas recebe dano se a DEF for maior que o ATK.</p>
            <p><strong>Vitória:</strong> Zerar a vida do oponente ou esgotar seu deck.</p>
        </div>
    </div>

    <audio id="alertSound" src="https://www.myinstants.com/media/sounds/alarm.mp3"></audio>

    <script>
        let currentValue = '10000';
        let history = ['10000'];
        let operationType = '';
        let firstNumber = '';
        let isNewNumber = true;

        function toggleCircle(circle) {
            circle.classList.toggle('on');
        }

        function nextTurn() {
            const circles = document.querySelectorAll('.circle');
            for (let circle of circles) {
                if (!circle.classList.contains('on')) {
                    circle.classList.add('on');
                    break;
                }
            }
        }

        function addNumber(num) {
            const display = document.getElementById('display');
            if (isNewNumber) {
                display.value = num;
                isNewNumber = false;
            } else {
                display.value += num;
            }
            currentValue = display.value;
        }

        function operation(op) {
            const display = document.getElementById('display');
            if (firstNumber === '') {
                firstNumber = currentValue;
            }
            operationType = op;
            isNewNumber = true;
        }

        function calculate() {
            const display = document.getElementById('display');
            let result;

            if (operationType && firstNumber !== '') {
                const secondNumber = currentValue;
                if (operationType === '+') {
                    result = parseInt(firstNumber) + parseInt(secondNumber);
                } else if (operationType === '-') {
                    result = parseInt(firstNumber) - parseInt(secondNumber);
                }
                
                display.value = result;
                currentValue = result.toString();
                updateHistory(result);
                firstNumber = result.toString();
                checkZero();
                isNewNumber = true;
            }
        }

        function clearDisplay() {
            const display = document.getElementById('display');
            display.value = '10000';
            currentValue = '10000';
            firstNumber = '';
            operationType = '';
            history = ['10000'];
            updateHistoryDisplay();
            isNewNumber = true;
            display.classList.remove('blink');
        }

        function back() {
            const display = document.getElementById('display');
            if (history.length > 1) {
                history.pop();
                const previousValue = history[history.length - 1];
                display.value = previousValue;
                currentValue = previousValue;
                firstNumber = previousValue;
                operationType = '';
                isNewNumber = true;
                updateHistoryDisplay();
                display.classList.remove('blink');
            }
        }

        function updateHistory(result) {
            if (history.length >= 5) {
                history.shift();
            }
            history.push(result.toString());
            updateHistoryDisplay();
        }

        function updateHistoryDisplay() {
            document.getElementById('history').textContent = history.join(', ');
        }

        function checkZero() {
            const display = document.getElementById('display');
            if (parseInt(currentValue) === 0) {
                display.classList.add('blink');
                document.getElementById('alertSound').play();
            } else {
                display.classList.remove('blink');
            }
        }
    </script>
</body>
</html>

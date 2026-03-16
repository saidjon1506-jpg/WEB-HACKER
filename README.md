<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SYSTEM TERMINAL v2.0</title>
    <style>
        body {
            background-color: #0a0a0a;
            color: #00ff00;
            font-family: 'Courier New', Courier, monospace;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        #terminal {
            width: 90%;
            max-width: 600px;
            background: rgba(0, 20, 0, 0.9);
            padding: 20px;
            border: 2px solid #00ff00;
            box-shadow: 0 0 20px #00ff00;
            border-radius: 10px;
            min-height: 300px;
        }

        .line {
            margin-bottom: 10px;
            white-space: pre-wrap;
        }

        .cursor {
            display: inline-block;
            width: 10px;
            height: 20px;
            background-color: #00ff00;
            animation: blink 1s infinite;
        }

        @keyframes blink {
            0%, 50% { opacity: 1; }
            51%, 100% { opacity: 0; }
        }

        input {
            background: transparent;
            border: none;
            color: #00ff00;
            font-family: inherit;
            font-size: 1.1em;
            outline: none;
            width: 100%;
        }
    </style>
</head>
<body>

<div id="terminal">
    <div id="output"></div>
    <div id="input-line">
        <span>$ </span><input type="text" id="cmd" autofocus>
    </div>
</div>

<script>
    const output = document.getElementById('output');
    const input = document.getElementById('cmd');

    const welcomeText = [
        "Initializing System...",
        "Loading Hackers Ethic modules...",
        "Establishing secure connection...",
        "Welcome, Saidjon. System is ready.",
        "Type 'help' for commands."
    ];

    function printLine(text, delay = 50) {
        const div = document.createElement('div');
        div.className = 'line';
        output.appendChild(div);
        let i = 0;
        const interval = setInterval(() => {
            div.textContent += text[i];
            i++;
            if (i === text.length) clearInterval(interval);
        }, delay);
    }

    welcomeText.forEach((text, index) => {
        setTimeout(() => printLine(text), index * 1000);
    });

    input.addEventListener('keypress', function (e) {
        if (e.key === 'Enter') {
            const cmd = this.value.toLowerCase();
            printLine("$ " + cmd);
            this.value = '';

            if (cmd === 'help') {
                printLine("> commands: status, clear, hack, about");
            } else if (cmd === 'status') {
                printLine("> System: Online. Security: Maximum.");
            } else if (cmd === 'hack') {
                printLine("> Accessing mainframe... Error: FireWall detected!");
            } else if (cmd === 'clear') {
                output.innerHTML = '';
            } else {
                printLine("> Unknown command: " + cmd);
            }
        }
    });
</script>
</body>
</html>

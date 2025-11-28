<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Animated Letter Display</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(45deg, #ffb6c1, #e6e6fa, #dda0dd, #ffb6c1);
            background-size: 400% 400%;
            animation: gradientShift 6s ease infinite;
            overflow: hidden;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .page {
            display: none;
            width: 100%;
            height: 100%;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }

        .page.active {
            display: flex;
        }

        #page1 {
            background: rgba(255, 182, 193, 0.9); /* Cool pink with transparency */
            border-radius: 15px;
            padding: 40px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            max-width: 400px;
            text-align: center;
            backdrop-filter: blur(10px);
        }

        #page1 h2 {
            color: #333;
            margin-bottom: 20px;
            font-weight: 300;
        }

        #page2 {
            position: relative;
            overflow: hidden;
        }

        #letterDisplay {
            font-size: 8em;
            color: #ff69b4;
            text-shadow: 0 0 20px #ff69b4, 0 0 40px #ff69b4, 0 0 60px #ff69b4;
            z-index: 10;
            position: relative;
            font-weight: bold;
        }

        .heart {
            position: absolute;
            width: 300px; /* Increased size */
            height: 300px; /* Increased size */
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 5;
        }

        .heart path {
            stroke: #ff69b4;
            stroke-width: 3; /* Slightly thicker stroke for better visibility */
            fill: none;
            stroke-linecap: round;
            stroke-linejoin: round;
            stroke-dasharray: 200; /* Approximate length of the heart path */
            stroke-dashoffset: 200;
            animation: drawHeart 3s ease-in-out forwards;
        }

        @keyframes drawHeart {
            to {
                stroke-dashoffset: 0;
            }
        }

        input {
            margin: 15px 0;
            padding: 15px;
            font-size: 1.2em;
            border: 2px solid #ff69b4;
            border-radius: 8px;
            text-align: center;
            width: 80%;
            max-width: 200px;
            text-transform: uppercase;
        }

        input:focus {
            outline: none;
            border-color: #87ceeb;
            box-shadow: 0 0 10px rgba(135, 206, 235, 0.5);
        }

        button {
            margin: 20px 0;
            padding: 15px 30px;
            font-size: 1.1em;
            background: linear-gradient(45deg, #ff69b4, #87ceeb);
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 7px 20px rgba(0,0,0,0.3);
        }

        button:active {
            transform: translateY(0);
        }
    </style>
</head>
<body>
    <div id="page1" class="page active">
        <h2>Enter an English Letter</h2>
        <input type="text" id="letterInput" maxlength="1" placeholder="A-Z" oninput="this.value = this.value.toUpperCase().replace(/[^A-Z]/g, '')">
        <button onclick="goToPage2()">Go to Display Page</button>
    </div>

    <div id="page2" class="page">
        <div id="letterDisplay"></div>
        <!-- Single heart that draws itself around the letter -->
        <svg class="heart" viewBox="0 0 24 24">
            <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
        </svg>
    </div>

    <script>
        function goToPage2() {
            const letter = document.getElementById('letterInput').value;
            if (letter && /^[A-Z]$/.test(letter)) {
                document.getElementById('letterDisplay').textContent = letter;
                document.getElementById('page1').classList.remove('active');
                document.getElementById('page2').classList.add('active');
            } else {
                alert('Please enter a single uppercase English letter (A-Z).');
            }
        }
    </script>
</body>
</html>

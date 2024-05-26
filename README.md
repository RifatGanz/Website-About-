<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Captcha Generator</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <style>
        body {
            background-image: url('https://telegra.ph/file/5da1667edef14a95baea2.jpg');
            background-size: cover;
            background-position: center;
        }

        .bubble {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            padding: 1rem 2rem;
            background-color: rgba(255, 0, 0, 0.8);
            border-radius: 8px;
            animation: fadeInOut 2s ease-in-out forwards;
        }

        @keyframes fadeInOut {
            0% {
                opacity: 0;
            }
            50% {
                opacity: 1;
            }
            100% {
                opacity: 0;
            }
        }
    </style>
</head>
<body class="text-white flex flex-col items-center justify-center h-screen">
    <div class="max-w-lg w-full p-8 rounded-lg bg-gray-800 bg-opacity-75 shadow-lg">
        <div class="flex flex-col items-center space-y-4">
            <h2 class="text-2xl font-semibold">Captcha Generator</h2>
            <div>
                <input type="text" readonly id="generated-captcha" class="w-full px-3 py-2 bg-gray-700 rounded-lg focus:outline-none focus:ring focus:ring-blue-500" placeholder="Generated Captcha">
            </div>
            <div>
                <input type="text" id="entered-captcha" class="w-full px-3 py-2 bg-gray-700 rounded-lg focus:outline-none focus:ring focus:ring-blue-500" placeholder="Enter the captcha..">
            </div>
            <button type="button" onclick="check()" class="w-full bg-blue-500 text-white py-2 rounded-lg hover:bg-blue-600 focus:outline-none focus:ring focus:ring-blue-500">
                Check
            </button>
            <div id="status" class="text-red-500"></div>
        </div>
    </div>

    <script>
        function generateCaptcha() {
            var captcha = Math.random().toString(36).substr(2, 6).toUpperCase(); // Generate random captcha
            document.getElementById('generated-captcha').value = captcha; // Set the generated captcha value
        }

        function check() {
            var generatedCaptcha = document.getElementById('generated-captcha').value;
            var enteredCaptcha = document.getElementById('entered-captcha').value.toUpperCase();

            if (generatedCaptcha === enteredCaptcha) {
                window.location.href = 'Souyuiscfilm.html'; // Redirect to a different page if captcha is correct
            } else {
                generateCaptcha(); // Generate new captcha
                document.getElementById('status').classList.remove('text-green-500');
                document.getElementById('status').classList.add('text-red-500');
                document.getElementById('status').innerHTML = 'Captcha is incorrect. Please try again.'; // Display error message
                showBubble(); // Show bubble message
            }
        }

        function showBubble() {
            var popups = ["TULIS YANG BENER", "TYPO WOI", "ALAH TYPO", "APALAH"];
            var randomIndex = Math.floor(Math.random() * popups.length);
            var bubble = document.createElement('div');
            bubble.textContent = popups[randomIndex];
            bubble.classList.add('bubble');
            document.body.appendChild(bubble);
            setTimeout(function() {
                bubble.style.opacity = '0'; // Fade out bubble
                setTimeout(function() {
                    bubble.remove(); // Remove bubble from DOM
                }, 1000); // After 1 second
            }, 2000); // After 2 seconds
        }

        // Generate captcha when page loads
        window.onload = generateCaptcha;
    </script>
</body>
</html>

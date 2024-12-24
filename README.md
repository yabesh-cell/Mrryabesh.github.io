<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Christmas Digital Gift</title>
    <style>
        body {
            font-family: "Arial", sans-serif;
            text-align: center;
            background: #2b5876;
            color: white;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
        }

        /* Snowflake effect */
        .snowflake {
            position: absolute;
            top: -10px;
            color: white;
            font-size: 30px;
            animation: fall 10s linear infinite;
        }

        @keyframes fall {
            0% { top: -10px; opacity: 1; }
            100% { top: 100vh; opacity: 0; }
        }

        /* Rest of the page */
        .container {
            margin-top: 50px;
            padding: 20px;
        }

        .gift {
            padding: 30px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
            position: relative;
            overflow: hidden;
            display: none;
            animation: fade-in 1.5s ease-out;
        }

        .gift-title {
            font-size: 2.2em;
            margin-bottom: 10px;
        }

        .verse, .wisher, .date {
            font-size: 1.2em;
            margin-bottom: 10px;
        }

        .uploaded-image {
            max-width: 120px;
            max-height: 120px;
            margin-top: 20px;
            border-radius: 50%;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
            border: 5px solid gold;
        }

        .button {
            padding: 15px 30px;
            background: linear-gradient(to right, #ff5e57, #ff9966);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1.2em;
            font-weight: bold;
            margin-top: 20px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
            transition: transform 0.2s ease;
        }

        .button:hover {
            background: linear-gradient(to right, #ff9966, #ff5e57);
            transform: scale(1.1);
        }

        .input, .input-file {
            width: 80%;
            max-width: 400px;
            padding: 10px;
            margin: 10px auto;
            border: none;
            border-radius: 5px;
            background: rgba(255, 255, 255, 0.1);
            color: white;
        }

        .input:focus, .input-file:focus {
            outline: none;
            box-shadow: 0 0 8px rgba(255, 255, 255, 0.8);
        }

        .button-submit {
            padding: 15px 30px;
            background: linear-gradient(to right, #ff5e57, #ff9966);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1.2em;
            font-weight: bold;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
            margin-top: 20px;
        }

        .button-submit:hover {
            background: linear-gradient(to right, #ff9966, #ff5e57);
        }

        /* Animations */
        @keyframes fade-in {
            from {
                opacity: 0;
                transform: scale(0.9);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

    </style>
</head>
<body>

    <!-- Snowflake effect -->
    <script>
        for (let i = 0; i < 100; i++) {
            let snowflake = document.createElement('div');
            snowflake.innerText = '❄';
            snowflake.classList.add('snowflake');
            snowflake.style.left = Math.random() * 100 + 'vw';
            snowflake.style.animationDuration = Math.random() * 5 + 5 + 's';
            snowflake.style.fontSize = Math.random() * 20 + 10 + 'px';
            document.body.appendChild(snowflake);
        }
    </script>

    <div class="container">
        <!-- First section: Form to enter data -->
        <h1>✨ Christmas Digital Gift ✨</h1>
        <p class="instructions">Fill in your details and upload an image to create a personalized Christmas gift. After submitting, you will see the animated gift.</p>
        <form id="form" onsubmit="submitForm(event)">
            <input type="text" id="name" placeholder="Enter your name" required class="input">
            <input type="number" id="age" placeholder="Enter your age" required class="input">
            <input type="file" id="image" accept="image/*" class="input-file">
            <button type="submit" class="button-submit">Generate Gift</button>
        </form>
        
        <!-- Second section: Animated gift -->
        <div id="gift" class="gift">
            <h2 id="gift-title" class="gift-title"></h2>
            <p id="verse" class="verse"></p>
            <p id="wisher" class="wisher"></p>
            <img id="uploaded-image" src="" alt="Uploaded Image" class="uploaded-image">
            <p id="date" class="date"></p>
            <p class="wisher">Best wishes from Yabesh Gotame</p>
            <button class="button" onclick="goBack()">Go Back</button>
        </div>
    </div>

    <script>
        // Function to handle the form submission
        function submitForm(event) {
            event.preventDefault();

            // Collect form data
            var name = document.getElementById("name").value;
            var age = document.getElementById("age").value;
            var image = document.getElementById("image").files[0];

            // Store data in localStorage
            localStorage.setItem("name", name);
            localStorage.setItem("age", age);
            if (image) {
                var reader = new FileReader();
                reader.onload = function(e) {
                    localStorage.setItem("image", e.target.result);
                };
                reader.readAsDataURL(image);
            }

            // Show the gift card and hide the form
            document.getElementById("gift").style.display = "block";
            document.getElementById("form").style.display = "none";

            // Call function to update gift card with data
            updateGiftCard();
        }

        // Function to update the gift card
        function updateGiftCard() {
            // Retrieve data from localStorage
            var name = localStorage.getItem("name");
            var age = localStorage.getItem("age");
            var image = localStorage.getItem("image");

            var verse = "For unto us a child is born, unto us a son is given. - Isaiah 9:6";
            var wisher = "Best Wishes, Yabesh Gotame";
            var date = new Date().toLocaleDateString();

            // Update the gift card with the collected data
            document.getElementById("gift-title").innerText = `Merry Christmas, ${name} (Age: ${age})! 🎄`;
            document.getElementById("verse").innerText = `"${verse}"`;
            document.getElementById("wisher").innerText = wisher;
            document.getElementById("date").innerText = `Date: ${date}`;

            // If an image is uploaded, display it
            if (image) {
                document.getElementById("uploaded-image").src = image;
            }
        }

        // Function to go back to the form
        function goBack() {
            // Show the form and hide the gift card
            document.getElementById("gift").style.display = "none";
            document.getElementById("form").style.display = "block";
            
            // Clear localStorage for next time
            localStorage.removeItem("name");
            localStorage.removeItem("age");
            localStorage.removeItem("image");
        }
    </script>

</body>
</html>

//1. HTML Structure (index.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS3 Transitions & Animations</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <h1>Welcome to the Animated Page</h1>

    <button id="animateButton" onclick="triggerAnimation()">Click to Animate</button>
    <div id="box"></div>

    <h2>Select Your Theme Preference:</h2>
    <form id="themeForm">
        <label for="themeSelect">Choose a theme:</label>
        <select id="themeSelect">
            <option value="light">Light</option>
            <option value="dark">Dark</option>
        </select>
        <button type="submit">Save Theme</button>
    </form>

    <script src="script.js"></script>
</body>
</html>

//2. CSS for Animations (styles.css)
/* Basic page styling */
body {
    font-family: Arial, sans-serif;
    text-align: center;
    padding: 50px;
}

h1 {
    font-size: 2.5em;
}

/* Styling the box that will animate */
#box {
    width: 100px;
    height: 100px;
    background-color: #3498db;
    margin: 20px auto;
    transition: transform 0.5s ease-in-out;
}

/* Animation for the box */
@keyframes bounce {
    0% {
        transform: translateY(0);
    }
    50% {
        transform: translateY(-30px);
    }
    100% {
        transform: translateY(0);
    }
}

/* Hover effect on button */
button:hover {
    background-color: #2980b9;
    cursor: pointer;
}

/* Apply animation when box is clicked */
.animate {
    animation: bounce 1s ease-in-out;
}

/* Light and Dark Themes */
body.light-theme {
    background-color: #f1f1f1;
    color: #333;
}

body.dark-theme {
    background-color: #333;
    color: #f1f1f1;
}

//
// Trigger animation on the #box element
function triggerAnimation() {
    let box = document.getElementById('box');
    box.classList.add('animate');

    // Remove the animation class after the animation completes to allow it to be triggered again
    setTimeout(() => {
        box.classList.remove('animate');
    }, 1000); // Duration matches the animation length
}

// Store theme preference in localStorage
function saveThemePreference() {
    let theme = document.getElementById('themeSelect').value;
    localStorage.setItem('theme', theme);
    applyTheme();
}

// Apply the saved theme from localStorage
function applyTheme() {
    let theme = localStorage.getItem('theme');
    if (theme) {
        document.body.classList.remove('light-theme', 'dark-theme');
        document.body.classList.add(theme + '-theme');
    }
}

// Load theme preference when the page loads
document.addEventListener('DOMContentLoaded', () => {
    applyTheme();

    // Attach event listener to theme form
    document.getElementById('themeForm').addEventListener('submit', (event) => {
        event.preventDefault(); // Prevent the form from reloading the page
        saveThemePreference();
    });
});



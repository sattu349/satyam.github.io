<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trip Tailor - Travel Planner</title>
    <link rel="stylesheet" href="styles.css">
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-firestore.js"></script>
    <script src="https://unpkg.com/cypress"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            color: #333;
        }
        header {
            background: #2c3e50;
            color: white;
            padding: 15px;
            text-align: center;
            position: sticky;
            top: 0;
            z-index: 1000;
        }
        nav ul {
            list-style: none;
            padding: 0;
            display: flex;
            justify-content: center;
        }
        nav ul li {
            margin: 0 15px;
        }
        nav ul li a {
            color: white;
            text-decoration: none;
            font-weight: bold;
        }
        section {
            padding: 20px;
            text-align: center;
        }
        #destination-list {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            padding: 20px;
        }
        .destination-card {
            background: white;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            cursor: pointer;
        }
        button {
            background: #3498db;
            color: white;
            border: none;
            padding: 10px 15px;
            cursor: pointer;
            border-radius: 5px;
        }
        button:hover {
            background: #2980b9;
        }
        #itinerary {
            margin-top: 20px;
            background: white;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .loading {
            font-size: 16px;
            font-weight: bold;
            color: #e74c3c;
        }
    </style>
</head>
<body>
    <header>
        <h1>Trip Tailor</h1>
        <nav>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#destinations">Destinations</a></li>
                <li><a href="#planner">AI Itinerary Planner</a></li>
            </ul>
        </nav>
    </header>
    <section id="home">
        <h2>Welcome to Trip Tailor</h2>
        <p>Plan your perfect trip with AI-powered itineraries and hidden gems.</p>
    </section>
    <section id="destinations">
        <h2>Popular Destinations</h2>
        <div id="destination-list"></div>
    </section>
    <section id="planner">
        <h2>AI Itinerary Planner</h2>
        <label for="destination">Choose a Destination:</label>
        <select id="destination"></select>
        <button onclick="generateItinerary()">Plan My Trip</button>
        <div id="itinerary" class="loading">Loading...</div>
    </section>
    <script>
        async function generateItinerary() {
            const destination = document.getElementById("destination").value;
            const itineraryElement = document.getElementById("itinerary");
            itineraryElement.innerHTML = "<span class='loading'>Generating itinerary...</span>";
            try {
                const response = await fetch("https://your-ai-backend.com/generate-itinerary", {
                    method: "POST",
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify({ destination })
                });
                if (!response.ok) {
                    throw new Error("Failed to fetch itinerary");
                }
                const data = await response.json();
                itineraryElement.innerHTML = `<h3>Your AI-Generated Itinerary:</h3><p>${data.itinerary}</p>`;
            } catch (error) {
                itineraryElement.innerHTML = "<span class='loading'>Error generating itinerary. Please try again.</span>";
                console.error("Error:", error);
            }
        }
    </script>
</body>
</html>

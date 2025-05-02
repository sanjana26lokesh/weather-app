# weather-app
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Offline Weather App</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * {
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', sans-serif;
            background: linear-gradient(to right, #74ebd5, #ACB6E5);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            padding: 20px;
        }
        
        .container {
            background: white;
            padding: 25px;
            border-radius: 15px;
            width: 100%;
            max-width: 400px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        input {
            width: 100%;
            padding: 10px;
            border-radius: 8px;
            border: 1px solid #ccc;
            margin-bottom: 10px;
            font-size: 1rem;
        }
        
        button {
            padding: 10px 20px;
            margin: 5px;
            font-size: 1rem;
            border: none;
            border-radius: 8px;
            background: #3498db;
            color: white;
            cursor: pointer;
        }
        
        button:hover {
            background: #2980b9;
        }
        
        .weather-info {
            margin-top: 20px;
            font-size: 1.1rem;
        }
        
        @media (max-width: 500px) {
            button {
                width: 100%;
                margin: 5px 0;
            }
        }
    </style>
</head>

<body>

    <div class="container">
        <h2>🌦️ Offline Weather App</h2>
        <input type="text" id="cityInput" placeholder="Enter city or place name">
        <div>
            <button onclick="showWeather()">Search</button>
            <button onclick="getLocation()">📍 My Location</button>
        </div>
        <div class="weather-info" id="weatherDisplay"></div>
    </div>

    <script>
        // Expanded simulated weather data
        const fakeWeatherData = {
            "bangalore": {
                temp: "26°C",
                condition: "Cloudy",
                humidity: "60%",
                wind: "3 m/s"
            },
            "mumbai": {
                temp: "32°C",
                condition: "Humid",
                humidity: "80%",
                wind: "2 m/s"
            },
            "delhi": {
                temp: "35°C",
                condition: "Sunny",
                humidity: "30%",
                wind: "5 m/s"
            },
            "mysore": {
                temp: "28°C",
                condition: "Partly Cloudy",
                humidity: "55%",
                wind: "4 m/s"
            },
            "kodagu": {
                temp: "22°C",
                condition: "Rainy",
                humidity: "90%",
                wind: "3 m/s"
            },
            "uttar pradesh": {
                temp: "34°C",
                condition: "Hot and Dry",
                humidity: "25%",
                wind: "6 m/s"
            },
            "kerala": {
                temp: "30°C",
                condition: "Rain Showers",
                humidity: "85%",
                wind: "2 m/s"
            },
            "america": {
                temp: "15°C",
                condition: "Snowy",
                humidity: "70%",
                wind: "4 m/s"
            },
            "south korea": {
                temp: "18°C",
                condition: "Clear",
                humidity: "45%",
                wind: "3 m/s"
            },
            "london": {
                temp: "12°C",
                condition: "Foggy",
                humidity: "80%",
                wind: "2 m/s"
            },
            "kashmir": {
                temp: "10°C",
                condition: "Cold",
                humidity: "65%",
                wind: "5 m/s"
            }
        };

        function showWeather() {
            const city = document.getElementById("cityInput").value.toLowerCase().trim();
            const display = document.getElementById("weatherDisplay");

            if (fakeWeatherData[city]) {
                const data = fakeWeatherData[city];
                display.innerHTML = `
        <p><strong>${city.toUpperCase()}</strong></p>
        <p>🌡️ Temp: ${data.temp}</p>
        <p>☁️ Condition: ${data.condition}</p>
        <p>💧 Humidity: ${data.humidity}</p>
        <p>🌬️ Wind: ${data.wind}</p>
      `;
            } else {
                display.innerHTML = `<p style="color:red;">Weather data for "${city}" is not available.</p>`;
            }
        }

        function getLocation() {
            const display = document.getElementById("weatherDisplay");
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(position => {
                    const lat = position.coords.latitude.toFixed(2);
                    const lon = position.coords.longitude.toFixed(2);
                    display.innerHTML = `
          <p><strong>Your Location</strong></p>
          <p>📍 Latitude: ${lat}</p>
          <p>📍 Longitude: ${lon}</p>
          <p>⚠️ Weather data for GPS location not available offline.</p>
        `;
                }, () => {
                    display.innerHTML = `<p style="color:red;">Could not get location.</p>`;
                });
            } else {
                display.innerHTML = `<p style="color:red;">Geolocation not supported by your browser.</p>`;
            }
        }
    </script>

</body>

</html>

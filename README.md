# Weather-checker
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Weather Checker</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #74ebd5, #9face6);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .weather-container {
      background-color: white;
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0px 8px 16px rgba(0, 0, 0, 0.2);
      text-align: center;
      max-width: 300px;
      width: 100%;
    }

    input, select {
      padding: 10px;
      width: 100%;
      margin-top: 15px;
      border-radius: 8px;
      border: 1px solid #ccc;
      box-sizing: border-box;
    }

    button {
      padding: 10px 20px;
      margin-top: 10px;
      background-color: #4a90e2;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      width: 100%;
    }

    #weatherResult {
      margin-top: 20px;
      font-size: 1.1em;
    }
  </style>
</head>
<body>
  <div class="weather-container">
    <h1>Weather Checker</h1>
    <input type="text" id="cityInput" placeholder="Enter city name" />
    <button onclick="getWeather()">Check Weather</button>
    <div id="weatherResult"></div>
  </div>

  <script>
    const apiKey = 'YOUR_API_KEY_HERE'; // Replace with your real OpenWeatherMap API key

    async function getWeather() {
      const city = document.getElementById('cityInput').value.trim();
      if (!city) {
        document.getElementById('weatherResult').innerHTML = '<p>Please enter a city name.</p>';
        return;
      }

      const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

      try {
        const response = await fetch(url);
        const data = await response.json();

        const result = document.getElementById('weatherResult');

        if (response.ok) {
          result.innerHTML = `
            <h2>${data.name}</h2>
            <p>Temperature: ${data.main.temp}°C</p>
            <p>Weather: ${data.weather[0].description}</p>
            <p>Humidity: ${data.main.humidity}%</p>
          `;
        } else {
          result.innerHTML = `<p>City not found. Please try again.</p>`;
        }
      } catch (error) {
        document.getElementById('weatherResult').innerHTML = `<p>Something went wrong. Please check your internet or try later.</p>`;
      }
    }
  </script>
</body>
</html>

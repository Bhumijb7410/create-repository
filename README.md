#CodeAlpha_Task1
<!DOCTYPE html>
<html>
<head>
  <title>Weather App</title>
  <style>
    body {
      font-family: Arial;
      text-align: center;
      margin-top: 50px;
    }
    input, button {
      padding: 10px;
      font-size: 16px;
    }
    #weather-info {
      margin-top: 20px;
      font-size: 18px;
    }
  </style>
</head>
<body>

  <h1>Weather Checker</h1>
  <input type="text" id="city" placeholder="Enter city name">
  <button onclick="getWeather()">Get Weather</button>

  <div id="weather-info"></div>

  <script>
    async function getWeather() {
      const apiKey = '7fa4e70c17f9449229798e9f7c00e075'; // Replace with your actual key
      const city = document.getElementById('city').value;
      const weatherInfo = document.getElementById('weather-info');

      if (!city) {
        weatherInfo.innerHTML = 'Please enter a city name.';
        return;
      }

      const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

      try {
        const response = await fetch(url);
        if (!response.ok) throw new Error('City not found');

        const data = await response.json();
        const temp = data.main.temp;
        const desc = data.weather[0].description;
        const name = data.name;

        weatherInfo.innerHTML = `Weather in <b>${name}</b>: ${temp}°C, ${desc}`;
      } catch (error) {
        weatherInfo.innerHTML = 'Error: ' + error.message;
      }
    }
  </script>

</body>
</html>
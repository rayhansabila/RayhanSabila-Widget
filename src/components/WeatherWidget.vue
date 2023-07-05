<template>
    <div class="weather-widget">
      <h2 class="widget-title">Weather Widget</h2>
      <div class="location-input">
        <label for="location">Enter Location:</label>
        <input type="text" id="location" v-model="location" />
        <button @click="fetchWeatherData">Get Weather</button>
      </div>
      <div v-if="weatherData" class="weather-data">
        <p class="location">Location: {{ weatherData.name }}</p>
        <p v-if="weatherData.main" class="temperature">
          Temperature: {{ weatherData.main.temp }}°C
        </p>
        <p v-if="weatherData.weather" class="description">
          Description: {{ weatherData.weather[0].description }}
        </p>
        <p v-if="weatherData.weather" class="additional-info">
          Current weather: <span class="weather-description">{{ weatherData.weather[0].description.toLowerCase() }}</span> with a temperature of <span class="temperature-value">{{ weatherData.main.temp }}°C</span>.
        </p>
      </div>
      <p v-else>Loading weather data...</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        location: '',
        weatherData: null
      };
    },
    methods: {
      async fetchWeatherData() {
        try {
          const apiKey = 'b7bfca7b27a3485144fea086c50d09dc';
          const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.location}&appid=${apiKey}`;
  
          const response = await fetch(apiUrl);
          const data = await response.json();
  
          this.weatherData = data;
        } catch (error) {
          console.error('Error fetching weather data:', error);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .weather-widget {
    border: 1px solid #ccc;
    padding: 20px;
    margin-bottom: 20px;
    text-align: center;
    background-color: #7895CB;
    font-family: 'Montserrat', sans-serif;
  }
  

  .widget-title {
    margin-top: 0;
    color: #333;
    font-size: 28px;
    font-weight: bold;
  }
  
  .location-input {
    margin-bottom: 10px;
  }
  
  .location-input label {
    font-size: 18px;
  }
  
  .location-input input[type="text"] {
    padding: 8px;
    border-radius: 4px;
    border: 1px solid #ccc;
    font-size: 16px;
  }
  
  .location-input button {
    padding: 8px 12px;
    border: none;
    background-color: #ff5722;
    color: #fff;
    font-size: 16px;
    font-weight: bold;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .location-input button:hover {
    background-color: #e64a19;
  }
  
  .weather-data {
    margin-top: 10px;
  }
  
  .location {
    font-size: 18px;
    font-weight: bold;
  }
  
  .temperature {
    font-size: 24px;
    color: #ff5722;
  }
  
  .description {
    font-size: 16px;
  }
  
  .additional-info {
    font-size: 14px;
    margin-top: 10px;
  }
  
  .weather-description {
    font-weight: bold;
  }
  
  .temperature-value {
    font-weight: bold;
    color: #ff5722;
  }
  </style>
  
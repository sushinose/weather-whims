<template>
  <div>
    <WeatherDisplay
      :weatherIcon="weatherIcon"
      :weatherComment="weatherComment"
      :temperature="temperature"
      :humorousComment="humorousComment"
    />
    <Forecast :forecast="forecast" />
  </div>
</template>

<script>
import WeatherDisplay from '@/components/WeatherDisplay.vue'
import Forecast from '@/components/Forecast.vue'
import axios from 'axios';



export default {
  name: 'Home',
  components: {
    WeatherDisplay,
    Forecast
  },
  data() {
    return {
      weatherIcon: '',
      weatherComment: '',
      temperature: null,
      humorousComment: '',
      forecast: [],
      city: 'Tokyo', // デフォルトの都市
      apiKey: 'c13cd41f54e67b37b8bdc24b6b1806cc' // OpenWeatherのAPIキー
      }
    },
    mounted() {
    this.fetchWeatherData();
  },
  methods: {
    async fetchWeatherData() {
      try {
        const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.apiKey}&units=metric`);
        const weatherData = response.data;
        this.temperature = weatherData.main.temp;
        this.weatherIcon = `http://openweathermap.org/img/wn/${weatherData.weather[0].icon}@2x.png`;
        this.weatherComment = weatherData.weather[0].description;
        this.humorousComment = this.getHumorousComment(weatherData.weather[0].main);
      } catch (error) {
        console.error("Error fetching weather data:", error);
      }
    },
    getHumorousComment(weatherMain) {
      const comments = {
        Clear: "It's so clear, you might just see a unicorn!",
        Clouds: "Cloudy with a chance of meatballs!",
        Rain: "Don't forget your rubber duck!",
        Snow: "Perfect day for a snowball fight!",
        Thunderstorm: "Thunderstorms are just sky's way of rock 'n' roll!",
        Drizzle: "It's like the sky is sprinkling magic.",
        Mist: "It's like a horror movie out there!"
      };
      return comments[weatherMain] || "Just another day!";
    }
  }
  }
  </script>

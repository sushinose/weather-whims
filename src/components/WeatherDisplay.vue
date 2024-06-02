<template>
  <div class="weather-display">
    <h2>Today's Weather</h2>
    <div class="weather-info" v-if="wetherIcon !== null && temperature !== null">
      <img :src="weatherIcon" alt="Weather icon"> 
      <p>{{ weatherComment }}</p>
      <p>{{ temperature }}°C - {{ humorousComment }}</p>
    </div>
    <div v-else>
      <p>Loading weather data...</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WeatherDisplay',
  props: {
    weatherIcon: String,
    weatherComment: String,
    temperature: Number,
    humorousComment: String
  }
}
</script>

<style scoped>
.weather-display {
  margin: 2em;
}
.weather-info {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.weather-info img {
  width: 100px;
  height: 100px;
}
</style>

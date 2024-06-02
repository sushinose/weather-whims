<template>
  <div class="forecast">
    <h2>Weekly Forecast</h2>
    <ul>
      <li v-for="day in forecast" :key="day.date">
        <p>{{ day.date }}</p>
        <p>{{ day.weather }}</p>
        <p>{{ day.comment }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Forecast',
  props: {
    forecast: Array
  }
}
</script>

<style scoped>
.forecast ul {
  list-style: none;
  padding: 0;
}
.forecast li {
  margin: 1em 0;
  padding: 1em;
  border: 1px solid #ccc;
  border-radius: 8px;
}
</style>

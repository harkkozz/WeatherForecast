<template>
  <div class="container">
    <div class="card main-card" v-if="weatherData != null">
      <h4 style="margin-top: 3%;">Weather in {{ city }}</h4>
      <img class="card-img-top" :src="weatherIcon" alt="Image">
      <h1>{{ temp }}&deg;C</h1><br>
      <!-- Button trigger modal -->
      <button type="button" class="btn btn-outline-info btn-sm" data-toggle="modal" data-target="#exampleModalCenter">
        <strong>View more info</strong>
      </button>
      <weather-preview-more :weatherData="weatherData"/>
    </div>
  </div>
</template>

<script>
import WeatherPreviewMore from './WeatherPreviewMore.vue'

export default {
  name: 'WeatherPreview',
  props: ['weatherData'],
  components: {
    WeatherPreviewMore
  },
  computed: {
    temp() {
      let temp
      temp = this.weatherData.main.temp - 273.15
      return Math.round(temp)
    },
    weatherIcon() {
      let icon = this.weatherData.weather[0].icon
      let url = `http://openweathermap.org/img/w/${icon}.png`
      return url
    },
    city() {
      return this.weatherData.name
    }
  }
}
</script>

<style scoped>
.card {
  width: 18rem;
  align-items: center;
  margin: 0 auto;
  margin-top: 3%;
  border-radius: 20px;
  padding: 10px;
}

img {
  width: 70px;
  height: 70px;
}
button {
  border-radius: 15px;
  margin-bottom: 5%;
}
</style>

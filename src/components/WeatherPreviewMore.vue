<template>
  <!-- Modal -->
<div class="modal fade" id="exampleModalCenter" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLongTitle">{{ city }} - {{ weatherDesc }}<img :src="weatherIcon" alt="Weather icon"> {{ temp }}&deg;C</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <h4>More info</h4>
        <hr>
        <div class="container">
          <p><strong>Min. Temp: {{ minTemp }}&deg;C </strong></p>
          <p><strong>Max. Temp: {{ maxTemp }}&deg;C </strong></p>
          <p><strong>Wind speed: {{ weatherWind }} m/s </strong></p>
          <p><strong>Pressure: {{ weatherPressure }} hpa </strong></p>
          <p><strong>Humidity: {{ humidity }} % </strong></p>
          <p><strong>Geo coords: [{{ geoLon }}, {{ geoLat }}] </strong></p>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'WeatherPreviewMore',
  props: ['weatherData'],
  computed: {
    temp() {
      let temp
      temp = this.weatherData.main.temp - 273.15
      return Math.round(temp)
    },
    minTemp() {
      let temp
      temp = this.weatherData.main.temp_min - 273.15
      return temp.toFixed(1)
    },
    maxTemp() {
      let temp
      temp = this.weatherData.main.temp_max - 273.15
      return temp.toFixed(1)
    },
    weatherIcon() {
      let icon = this.weatherData.weather[0].icon
      let url = `http://openweathermap.org/img/w/${icon}.png`
      return url
    },
    weatherDesc() {
      return this.weatherData.weather[0].main
    },
    city() {
      return this.weatherData.name
    },
    weatherWind() {
      return this.weatherData.wind.speed
    },
    weatherPressure() {
      return this.weatherData.main.pressure
    },
    geoLon() {
      return this.weatherData.coord.lon
    },
    geoLat() {
      return this.weatherData.coord.lat
    },
    humidity() {
      return this.weatherData.main.humidity
    }
  }
}
</script>

<style scoped>

</style>

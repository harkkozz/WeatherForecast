<template>
  <div id="app">
    <h1 style="margin-bottom: 2%;">Weather Forecast</h1>
    <search-bar @citySearch="onTextSearch"/>
    <div class="alert alert-danger" role="alert" v-if="alert">
      Check the value you entered.
    </div>
    <img src="./assets/loading.gif" alt="" v-if="loading" width="50" height="50">
    <weather-preview :weatherData="cityWeatherData"/>
  </div>
</template>

<script>
import axios from 'axios'
import SearchBar from './components/SearchBar'
import WeatherPreview from './components/WeatherPreview'

export default {
  name: 'app',
  data() {
    return {
      city: null,
      cityWeatherData: null,
      loading: false,
      alert: false
    }
  },
  components: {
    SearchBar,
    WeatherPreview
  },
  methods: {
    onTextSearch(citySearch) {
      this.loading = true
      axios.get('', {
        params: {
          q: citySearch,
          APPID: 'cc1659552aca64ff72d7b8631632dc6a',
        }
      })
      .then(response => {
        this.loading = false
        this.cityWeatherData = response.data
        this.alert = false
      })
      .catch(() => {
        this.loading = false
        this.alert = true
      })
    }
  }
}
</script>

<style>
body {
  margin: 0 auto;
  padding: 0;
  height: 100%;
  background: url('./assets/bgweather.jpg');
  background-repeat: no-repeat;
  background-size: cover;
}
@media only screen and (max-width: 1024px){
  body {
    background-size: initial
  }
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.alert {
  margin: 0 30%;
}
</style>

<template>
      <div v-if="!weather">Загрузка...</div>
      <div v-else style="display: flex; justify-content: space-around;">
        <weather-card 
            :cloudness="weather['list'][0]['clouds']['all']" 
            :temperature="weather['list'][0]['main']['temp']"
            :wind="weather['list'][0]['wind']['speed']" 
            :humidity="weather['list'][0]['main']['humidity']" 
            :pressure="weather['list'][0]['main']['pressure']">
            </weather-card>
            <weather-card 
            :cloudness="weather['list'][1]['clouds']['all']" 
            :temperature="weather['list'][1]['main']['temp']"
            :wind="weather['list'][1]['wind']['speed']" 
            :humidity="weather['list'][1]['main']['humidity']" 
            :pressure="weather['list'][1]['main']['pressure']">
            </weather-card>
            <weather-card 
            :cloudness="weather['list'][2]['clouds']['all']" 
            :temperature="weather['list'][2]['main']['temp']"
            :wind="weather['list'][2]['wind']['speed']" 
            :humidity="weather['list'][2]['main']['humidity']" 
            :pressure="weather['list'][2]['main']['pressure']">
            </weather-card>
            <weather-card 
            :cloudness="weather['list'][3]['clouds']['all']" 
            :temperature="weather['list'][3]['main']['temp']"
            :wind="weather['list'][3]['wind']['speed']" 
            :humidity="weather['list'][3]['main']['humidity']" 
            :pressure="weather['list'][3]['main']['pressure']">
            </weather-card>
            <weather-card 
            :cloudness="weather['list'][4]['clouds']['all']" 
            :temperature="weather['list'][4]['main']['temp']"
            :wind="weather['list'][4]['wind']['speed']" 
            :humidity="weather['list'][4]['main']['humidity']" 
            :pressure="weather['list'][4]['main']['pressure']">
        </weather-card>
      </div>
</template>

<script>
import WeatherCard from './WeatherCard.vue'

export default {
  components: {
    "weather-card": WeatherCard,
  },
  props: {
    lat: Number,
    lon: Number
  },
  data() {
    return {
      weather: null,
    }
  },
  methods: {
    getWeather() {
        console.log("cl");
      fetch(`https://api.openweathermap.org/data/2.5/forecast?lat=${this.lat}&lon=${this.lon}&appid=de97e3b38fb8be62d9aa634927b0b35c&units=metric`)
        .then(resp => resp.json())
        .then(json => {
          this.weather = json;
        })
    }
  },
  mounted() {
    this.getWeather()
  }
}
</script>

<style>

</style>
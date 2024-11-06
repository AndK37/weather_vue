<template>
  <button @click="changeUnits">°{{ currentUnits }}</button>
  <select id="sel" name="" v-model="selectedCity" @change="getWeather">
    <option id="op" v-for="(v, k) in cities" :value="k" :key="k">{{ v["City"] }}</option>
  </select>
  <h1>{{ cities[selectedCity] }}</h1>
  <div v-if="!weatherNow">Загрузка...</div>
  <div v-else>
    <weather-card class="main-card"
      :cloudness="weatherNow['clouds']['all']" 
      :temperature="tmp"
      :wind="weatherNow['wind']['speed']" 
      :humidity="weatherNow['main']['humidity']" 
      :pressure="weatherNow['main']['pressure']" 
      :desc="weatherNow['weather'][0]['description']" 
      :icon="weatherNow['weather'][0]['icon']" 
      :units="currentUnits">
    </weather-card>
    <card-list :weather="weatherForecast" :units="currentUnits">
    </card-list>
  </div>


</template>
<script>
import CardList from './components/CardList.vue'
import WeatherCard from './components/WeatherCard.vue'
export default {
  components: {
    "card-list": CardList,
    "weather-card": WeatherCard
  },
  data() {
    return {
      weatherNow: null,
      weatherForecast: null,
      cities: [],
      selectedCity: 0,
      currentUnits: 'C'
    }
  },
  methods: {
    getWeather() {
      fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${this.cities[this.selectedCity]?.Lat}&lon=${this.cities[this.selectedCity]?.Lon}&appid=de97e3b38fb8be62d9aa634927b0b35c&units=metric`)
        .then(resp => resp.json())
        .then(json => {
          this.weatherNow = json;
          this.tmp = this.weatherNow['main']['temp'].toFixed(0)
        })
      fetch(`https://api.openweathermap.org/data/2.5/forecast?lat=${this.cities[this.selectedCity]?.Lat}&lon=${this.cities[this.selectedCity]?.Lon}&appid=de97e3b38fb8be62d9aa634927b0b35c&units=metric`)
        .then(resp => resp.json())
        .then(json => {
          this.weatherForecast = json;
          for (let i = 0; i < 40; i++) {
            this.weatherForecast['list'][i]['main']['temp'] = (this.weatherForecast['list'][i]['main']['temp']).toFixed(0)
          }
      })
      
    },
    changeUnits() {
      if (this.currentUnits == 'C') {
        this.currentUnits = 'F'
        this.tmp = ((this.tmp * 9/5) + 32).toFixed(0)
        for (let i = 0; i < 40; i++) {
          this.weatherForecast['list'][i]['main']['temp'] = ((this.weatherForecast['list'][i]['main']['temp'] * 9/5) + 32).toFixed(0)
        }
      }
      else if (this.currentUnits == 'F') {
        this.currentUnits = 'C'
        this.tmp = ((this.tmp - 32) * 5/9).toFixed(0)
        for (let i = 0; i < 40; i++) {
          this.weatherForecast['list'][i]['main']['temp'] = ((this.weatherForecast['list'][i]['main']['temp'] - 32) * 5/9).toFixed(0)
        }
      }
    }
  },
  mounted() {
    fetch("cities.json")
      .then(resp => resp.json())
      .then(json => {
        this.cities = json;
      })
  }
}
</script>

<style>
html, body {
  height: 100vh;

}

body {
  background: rgb(82, 153, 211);
  background: linear-gradient(180deg, rgb(59, 127, 182) 0%, rgb(54, 102, 122) 100%);
  background-repeat: no-repeat;
  height: 100%;
  padding-left: 5vw;
  padding-right: 5vw;
}

select {
  background: rgba(255, 255, 255, 0.2);
    border-radius: 16px;
    box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
    backdrop-filter: blur(5px);
    -webkit-backdrop-filter: blur(5px);
    border: 1px solid rgba(255, 255, 255, 0.3);
    border-radius: 10px;
    font-size: 32px;
    color: aliceblue;
}
option {
  background-color: rgb(82, 153, 211);
  

}
button {
  background: rgba(255, 255, 255, 0.2);
    border-radius: 16px;
    box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
    backdrop-filter: blur(5px);
    -webkit-backdrop-filter: blur(5px);
    border: 1px solid rgba(255, 255, 255, 0.3);
    border-radius: 10px;
    font-size: 32px;
    color: aliceblue;
    width: 64px;
}
</style>

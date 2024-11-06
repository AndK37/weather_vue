<template>
  <select id="sel" name="" v-model="selectedCity" @change="getWeather">
    <option id="op" v-for="(v, k) in cities" :value="k" :key="k">{{ v["City"] }}</option>
  </select>
  <h1>Город {{ cities[selectedCity]?.City }} Широта {{ cities[selectedCity]?.Lat }} Долгота {{ cities[selectedCity]?.Lon
    }}</h1>
  <div v-if="!weather">Загрузка...</div>
  <div v-else>
    <weather-card class="main-card" 
      :cloudness="weather['clouds']['all']" 
      :temperature="weather['main']['temp']"
      :wind="weather['wind']['speed']" 
      :humidity="weather['main']['humidity']" 
      :pressure="weather['main']['pressure']">
    </weather-card>
    <card-list :lat="cities[selectedCity]?.Lat" :lon="cities[selectedCity]?.Lon">
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
      weather: null,
      cities: [],
      selectedCity: 0
    }
  },
  methods: {
    getWeather() {
      console.log("ap");
      fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${this.cities[this.selectedCity]?.Lat}&lon=${this.cities[this.selectedCity]?.Lon}&appid=de97e3b38fb8be62d9aa634927b0b35c&units=metric`)
        .then(resp => resp.json())
        .then(json => {
          this.weather = json;
        })
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
  height: 100%;

}

body {
  background: rgb(82, 153, 211);
  background: linear-gradient(180deg, rgba(82, 153, 211, 1) 0%, rgba(75, 136, 162, 1) 100%);
  background-repeat: no-repeat;
  height: 100%;
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

</style>

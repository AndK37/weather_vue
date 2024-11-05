<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <select name="" v-model="selectedCity" @change="getWeather">
    <option v-for="(v, k) in cities" :value="k" :key="k">{{ v["City"] }}</option>
  </select>
  <h1>Город {{ cities[selectedCity]?.City }} Широта {{ cities[selectedCity]?.Lat }} Долгота {{ cities[selectedCity]?.Lon
    }}</h1>
  <div v-if="!weather">Загрузка...</div>
  <div v-else>
    <card-list :lat="cities[selectedCity]?.Lat" :lon="cities[selectedCity]?.Lon">

    </card-list>
  </div>


</template>
<script>
import CardList from './components/CardList.vue'

export default {
  components: {
    "card-list": CardList,
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
html {
  height: 100%;
}

body {
  background: rgb(82, 153, 211);
  background: linear-gradient(180deg, rgba(82, 153, 211, 1) 0%, rgba(75, 136, 162, 1) 100%);
  background-repeat: no-repeat;
  height: 100%;
}
</style>

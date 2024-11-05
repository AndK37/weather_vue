<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <select name="" v-model="selectedCity" @change="getWeather">
    <option v-for="(v,k) in city" :value="k" :key="k">{{ v["City"] }}</option>
  </select>
  <h1>Город {{ city[selectedCity]?.City }} Широта {{ city[selectedCity]?.Lat }} Долгота {{ city[selectedCity]?.Lon }}</h1>
  <div v-if="!weather">Загрузка...</div>
  <div v-else>
    <ul>
    <li>Сейчас {{weather["main"]["temp"]}} градусов</li>
    <li></li>
    <li></li>
    <li>Влажность {{weather["main"]["humidity"]}}</li>
    <li>Давление {{weather["main"]["pressure"]}} Па</li>
    <li>Ветер {{weather["wind"]["speed"]}} м/с</li>
  </ul>
  </div>

</template>

<script>
export default {
  name: 'App',
  components: {
    // HelloWorld
  }, 
  data() {
    return {
      weather:null,
      city: [],
      selectedCity: 0,
    }
  },
  mounted() {
    fetch("cities.json")
    .then(resp=>resp.json())
    .then(json=>{
        this.city=json;
    })
  },
  methods: {
    getWeather() {
      fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${this.city[this.selectedCity]?.Lat}&lon=${this.city[this.selectedCity]?.Lon}&appid=de97e3b38fb8be62d9aa634927b0b35c&units=metric`)
      .then(resp=>resp.json())
      .then(json=>{
        this.weather=json;
      })
    }
  }
}
</script>
<style>

</style>

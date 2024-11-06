<template>
      <div v-if="!weather">Загрузка...</div>
      <div v-else class="list">
        <img @click="prevPage" v-show="listPage != 0" src="../assets/chevron_right_64dp_E8EAED_FILL0_wght400_GRAD0_opsz48.svg" alt="" style="rotate: 180deg; cursor: pointer;">
        <div class="list__item" v-for="n in 5" :key="n">
          <span class="list__time">{{ 	new Date(Number(weather['list'][n - 1 + listPage * 5]['dt']) * 1000).getHours() }}:00</span>
          <weather-card 
            :cloudness="weather['list'][n - 1 + listPage * 5]['clouds']['all']" 
            :temperature="weather['list'][n - 1 + listPage * 5]['main']['temp']"
            :wind="weather['list'][n - 1 + listPage * 5]['wind']['speed']" 
            :humidity="weather['list'][n - 1 + listPage * 5]['main']['humidity']" 
            :pressure="weather['list'][n - 1 + listPage * 5]['main']['pressure']" 
            :desc="weather['list'][n - 1 + listPage * 5]['weather'][0]['description']" 
            :icon="weather['list'][n - 1 + listPage * 5]['weather'][0]['icon']" 
            :units="units">
          </weather-card>
        </div>
        <img @click="nextPage" v-show="listPage != 7" src="../assets/chevron_right_64dp_E8EAED_FILL0_wght400_GRAD0_opsz48.svg" alt="" style="cursor: pointer;">
      </div>
      <div class="pages">
        {{ listPage + 1 }} / 7
      </div>
</template>

<script>
import WeatherCard from './WeatherCard.vue'

export default {
  components: {
    "weather-card": WeatherCard,
  },
  props: {
    weather: JSON,
    units: String,
  },
  data() {
    return {
      listPage:0
    }
  },
  methods: {
    prevPage() {
      if (this.listPage == 0) {
        this.listPage = 0
      } else {
        this.listPage--
      }
    },
    nextPage() {
      if (this.listPage == 7) {
        this.listPage = 7
      } else {
        this.listPage++
      }
    }
  },
}
</script>

<style>
.list {
  display: flex; 
  justify-content: space-around;
  flex-wrap: wrap;
}

.list__item {
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: translate 0.5s;
}

.list__item:hover {
  translate: 0px -10px;
}

.list__time {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 48px;
  color: aliceblue;
  margin-bottom: 5px;
}
.pages {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 48px;
  color: aliceblue;
  display: flex;
  justify-content: center;
}
</style>
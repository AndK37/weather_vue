<template>
  <div class="app">
    <my-header ref="header" :currentUnits="currentUnits" :cities="cities"></my-header>
    <div class="app_top">
      <div class="app__load" v-if="!weatherNow">
        Загрузка...</div>
      <div v-else>
        <weather-main-card class="main-card" :weatherNow="weatherNow" :units="currentUnits" />
        <feature-list></feature-list>
      </div>
    </div>
    <div class="app_bot">
      <div class="app__load" v-if="!weatherNow">
        Загрузка...</div>
      <div v-else>
        <card-list :weather="weatherForecast" :units="currentUnits" />
      </div>
    </div>
  </div>
</template>
<script>
import CardList from './components/CardList.vue';
import MyHeader from './components/MyHeader.vue';
import WeatherMainCard from './components/WeatherMainCard.vue';
import FeatureList from './components/FeatureList.vue';
export default {
  components: {
    "card-list": CardList,
    "my-header": MyHeader,
    "weather-main-card": WeatherMainCard,
    "feature-list": FeatureList
  },
  data() {
    return {
      weatherNow: null,
      weatherForecast: null,
      cities: [],
      currentUnits: 'C'
    }
  },
  methods: {
    getWeather() {
      fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${this.$refs.header.cities[this.$refs.header.selectedCity]?.Lat}&lon=${this.$refs.header.cities[this.$refs.header.selectedCity]?.Lon}&appid=de97e3b38fb8be62d9aa634927b0b35c&units=metric&lang=ru`)
        .then(resp => resp.json())
        .then(json => {
          this.weatherNow = json;
          this.weatherNow['main']['temp'] = this.weatherNow['main']['temp'].toFixed(0)
        })
      fetch(`https://api.openweathermap.org/data/2.5/forecast?lat=${this.$refs.header.cities[this.$refs.header.selectedCity]?.Lat}&lon=${this.$refs.header.cities[this.$refs.header.selectedCity]?.Lon}&appid=de97e3b38fb8be62d9aa634927b0b35c&units=metric&lang=ru`)
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
        this.weatherNow['main']['temp'] = ((this.weatherNow['main']['temp'] * 9 / 5) + 32).toFixed(0)
        for (let i = 0; i < 40; i++) {
          this.weatherForecast['list'][i]['main']['temp'] = ((this.weatherForecast['list'][i]['main']['temp'] * 9 / 5) + 32).toFixed(0)
        }
      } else if (this.currentUnits == 'F') {
        this.currentUnits = 'C'
        this.weatherNow['main']['temp'] = ((this.weatherNow['main']['temp'] - 32) * 5 / 9).toFixed(0)
        for (let i = 0; i < 40; i++) {
          this.weatherForecast['list'][i]['main']['temp'] = ((this.weatherForecast['list'][i]['main']['temp'] - 32) * 5 / 9).toFixed(0)
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
  },



}
</script>

<style>
html,
body {
  margin: 0;
  height: 100%;
}

.app {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
  padding-left: 5vw;
  padding-right: 5vw;
  gap: 40px
}

.app__load {
  display: flex;
  justify-content: center;
  color: aliceblue;
  font-size: 8rem;
  font-family: Arial, Helvetica, sans-serif;
}



body {
  background-color: rgb(82, 153, 211);
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

/* 2xl */
@media (max-width: 1536px) {
  .app__load {
    font-size: 6rem;
  }
}

/* xl */
@media (max-width: 1280px) {
  .app__load {
    font-size: 5rem;
  }
}

/* lg */
@media (max-width: 1024px) {
  .app__load {
    font-size: 4rem;
  }
}

/* md */
@media (max-width: 768px) {
  .app__load {
    font-size: 3rem;
  }
}

/* sm */
@media (max-width: 640px) {
  .app__load {
    font-size: 2rem;
  }
}

/* xs */
@media (max-width: 475px) {
  .app__load {
    font-size: 1rem;
  }
}
</style>

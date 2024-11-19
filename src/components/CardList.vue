<template>
  <div class="cardList">
    <img @click="prevPage" v-if="listPage != 1" src="../assets/chevron_right_64dp_E8EAED_FILL0_wght400_GRAD0_opsz48.svg"
      alt="" style="rotate: 180deg; cursor: pointer; margin-right: 20px;">
    <img v-else width="68px">
    <div v-if="!weather">Загрузка...</div>
    <div v-else class="list">
      <div class="list__item" v-for="n in 5" :key="n">
        <span class="list__time">{{ new Date(Number(weather['list'][pagination(n)]['dt']) * 1000).getHours()
          }}:00</span>
        <weather-card :cloudness="weather['list'][pagination(n)]['clouds']['all']"
          :temperature="weather['list'][pagination(n)]['main']['temp']"
          :wind="weather['list'][pagination(n)]['wind']['speed']"
          :humidity="weather['list'][pagination(n)]['main']['humidity']"
          :pressure="weather['list'][pagination(n)]['main']['pressure']"
          :desc="weather['list'][pagination(n)]['weather'][0]['description']"
          :icon="weather['list'][pagination(n)]['weather'][0]['icon']" :units="units">
        </weather-card>
      </div>
    </div>
    <img @click="nextPage" v-if="listPage != 7" src="../assets/chevron_right_64dp_E8EAED_FILL0_wght400_GRAD0_opsz48.svg"
      alt="" style="cursor: pointer; margin-left: 20px;">
    <img v-else width="68px">

  </div>
  <div class="pages">
    {{ listPage }} / 7
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
      listPage: 1
    }
  },
  methods: {
    prevPage() {
      var element = document.getElementsByClassName('list');
      element[0].classList.add('prev-page-anim');
      element[0].addEventListener("animationend", function () {
        element[0].classList.remove('prev-page-anim');
      })
      if (this.listPage == 1) {
        this.listPage = 1
      } else {
        this.listPage--
      }
    },
    nextPage() {
      var element = document.getElementsByClassName('list');
      element[0].classList.add('next-page-anim');
      element[0].addEventListener("animationend", function () {
        element[0].classList.remove('next-page-anim');
      })
      if (this.listPage == 7) {
        this.listPage = 7
      } else {
        this.listPage++
      }
    },
    pagination(n) {
      return n - 1 + this.listPage * 5;
    }
  },
}
</script>

<style scoped>
.cardList {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.list {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
  flex: 1 1 0px;
}

.list__item {
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: translate 0.5s;
  animation-timing-function: cubic-bezier(0.1, -0.6, 0.2, 0);
}

.next-page-anim {
  animation-name: cssAnimation;
  animation-duration: 1.2s;
  animation-iteration-count: 1;
  animation-timing-function: cubic-bezier(0.68, -0.6, 0.32, 1.6);
  animation-fill-mode: forwards;
}

@keyframes cssAnimation {
  0% {}

  25% {
    transform: translate(-100vw);
  }

  50% {
    opacity: 0;
  }

  75% {
    transform: translate(100vw);

  }

  100% {
    opacity: 1;
    transform: translate(0vw);
  }
}

.prev-page-anim {
  animation-name: revcssAnimation;
  animation-duration: 1.2s;
  animation-iteration-count: 1;
  animation-timing-function: cubic-bezier(0.68, -0.6, 0.32, 1.6);
  animation-fill-mode: forwards;

}

@keyframes revcssAnimation {
  0% {}

  25% {
    transform: translate(100vw);
  }

  50% {
    opacity: 0;
  }

  75% {
    transform: translate(-100vw);

  }

  100% {
    opacity: 1;
    transform: translate(0vw);
  }
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

/* 2xl */
@media (max-width: 1536px) {}

/* xl */
@media (max-width: 1280px) {
  .list__time {
    font-size: 2rem;
  }
}

/* lg */
@media (max-width: 1024px) {}

/* md */
@media (max-width: 768px) {
  .list__time {
    font-size: 1rem;
  }
}

/* sm */
@media (max-width: 640px) {}

/* xs */
@media (max-width: 475px) {}
</style>
<template>
    <div class="card">
        <div class="card_top">
            <div class="card__main-info">
                <img v-bind:src="'https://openweathermap.org/img/wn/'+ weatherNow['weather'][0]['icon'] +'@4x.png'" alt="no icon" height="128px" width="128px"/>
                <span class="card_bot">{{ weatherNow['weather'][0]['description'] }}</span>
            </div>
            <div class="card__main-info">
                <span>{{ weatherNow['main']['temp'] }} °{{ units }}</span>
            </div>

        </div>
        <div class="card_bot">
            <div class="card__sub-info card__sub-info_1">
                <span>Ветер</span>
                <span>Влажность</span>
                <span>Давление</span>
            </div>
            <div class="card__sub-info card__sub-info_2">
                <span>{{ weatherNow['wind']['speed'] }}</span>
                <span>{{ weatherNow['main']['humidity'] }}</span>
                <span>{{ weatherNow['main']['pressure'] }}</span>
            </div>
            <div class="card__sub-info card__sub-info_3">
                <span>м/с</span>
                <span>%</span>
                <span>гПа</span>
            </div>
        </div>
    </div>

</template>

<script>
export default {
    props: {
        weatherNow: JSON,
        units: String
    }
}
</script>

<style scoped>
body {
    background-color: #202020;
}

.card {
    background: rgba(255, 255, 255, 0.2);
    border-radius: 16px;
    box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
    backdrop-filter: blur(5px);
    -webkit-backdrop-filter: blur(5px);
    border: 1px solid rgba(255, 255, 255, 0.3);
    border-radius: 10px;
    transition: ease;
    padding: 3px;
    width: 50vw;
    height: max-content;
    color: aliceblue;
    padding: 5px;
    font-family: Arial, Helvetica, sans-serif;
}

.card_top {
    font-size: 10rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 5px;
    border-bottom: solid white 3px;
}

.card_bot {
    display: flex;
    justify-content: space-between;
    font-size: 4rem;
    padding: 5px;
}

.card__sub-info {
    display: flex;
    flex-direction: column;
}
.card__sub-info_1, .card__sub-info_2 {
    margin-right: 30px;
}
.card__sub-info_2, .card__sub-info_3 {
    text-align: end;
}
.card__main-info {
    display: flex;
    flex-direction: column;
}
/* 2xl */
@media (max-width: 1660px) {
    .card_top {
        font-size: 6rem;
    }
    .card_bot {
        font-size: 3rem;
    }
}

/* xl */
@media (max-width: 1400px) {
    .card_top {
        font-size: 4rem;
    }
    .card_bot {
        font-size: 2rem;
    }
}

/* lg */
@media (max-width: 780px) {
    .card_top {
        font-size: 2rem;
    }
    .card_bot {
        font-size: 1rem;
    }
}

/* md */
@media (max-width: 768px) {

}

/* sm */
@media (max-width: 640px) {

}

/* xs */
@media (max-width: 475px) {

}
</style>
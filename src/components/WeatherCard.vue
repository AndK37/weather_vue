<template>
    <div class="card">
        <div class="card_top">
            <div class="card__main-info">
                <img v-bind:src="'https://openweathermap.org/img/wn/' + icon + '@4x.png'" alt="no icon" height="64px"
                    width="64px" />
                <span class="card_bot">{{ desc }}</span>
            </div>
            <div class="card__main-info">
                <span>{{ temperature }} °{{ units }}</span>
            </div>

        </div>
        <div class="card_bot">
            <div class="card__sub-info card__sub-info_1">
                <span>{{ $t("wind") }}</span>
                <span>{{ $t("humidity") }}</span>
                <span>{{ $t("pressure") }}</span>
            </div>
            <div class="card__sub-info card__sub-info_2">
                <span>{{ wind }}</span>
                <span>{{ humidity }}</span>
                <span>{{ pressure }}</span>
            </div>
            <div class="card__sub-info card__sub-info_3">
                <span>{{ $t("speed") }}</span>
                <span>%</span>
                <span>{{ $t("pres") }}</span>
            </div>
        </div>
    </div>

</template>

<script>
export default {
    props: {
        temperature: String,
        cloudness: Number,
        wind: Number,
        humidity: Number,
        pressure: Number,
        desc: String,
        icon: String,
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
    width: max-content;
    height: max-content;
    color: aliceblue;
    padding: 5px;
    font-family: Arial, Helvetica, sans-serif;
}

.card_top {
    font-size: 64px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 5px;
    border-bottom: solid white 3px;
}

.card_bot {
    display: flex;
    justify-content: space-between;
    font-size: 32px;
    padding: 5px;
}

.card__sub-info {
    display: flex;
    flex-direction: column;
}

.card__sub-info_1,
.card__sub-info_2 {
    margin-right: 30px;
}

.card__sub-info_2,
.card__sub-info_3 {
    text-align: end;
}

.card__main-info {
    display: flex;
    flex-direction: column;
}

/* 2xl */
@media (max-width: 1536px) {
    .card_top {
        font-size: 4rem;
    }
    .card_bot {
        font-size: 2rem;
    }
}

/* xl */
@media (max-width: 1280px) {

}

/* lg */
@media (max-width: 1024px) {
    .card_top {
        font-size: 2rem;
    }
    .card_bot {
        font-size: 1rem;
    }
}

/* md */
@media (max-width: 768px) {}

/* sm */
@media (max-width: 640px) {
    .card_top {
        font-size: 1rem;
    }
}

/* xs */
@media (max-width: 475px) {}
</style>
<template>
    <div class="card">
        <div class="card_top">
            <div class="card__main-info" v-if="cloudness > 66">
                <img src="../assets/cloudness/cloud_64dp_E8EAED_FILL0_wght400_GRAD0_opsz48.svg" height="64px">
                <span style="font-size: 32px;">Облачно</span>
            </div>
            <div class="card__main-info" v-else-if="cloudness > 33">
                <img src="../assets/cloudness/partly_cloudy_day_64dp_E8EAED_FILL0_wght400_GRAD0_opsz48.svg" height="64px">
                <span style="font-size: 32px;">Част. облачность</span>
            </div>
            <div class="card__main-info" v-else-if="cloudness > 0">
                <img src="../assets/cloudness/clear_day_64dp_E8EAED_FILL0_wght400_GRAD0_opsz48.svg" height="64px">
                <span style="font-size: 32px;">Ясно</span>
            </div>
            <div class="card__main-info">
                <span>{{ temperature }} °</span>
            </div>

        </div>
        <div class="card_bot">
            <div class="card__sub-info card__sub-info_1">
                <span>Ветер</span>
                <span>Влажность</span>
                <span>Давление</span>
            </div>
            <div class="card__sub-info card__sub-info_2">
                <span>{{ wind }}</span>
                <span>{{ humidity }}</span>
                <span>{{ pressure }}</span>
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
        temperature: Number,
        cloudness: Number,
        wind: Number,
        humidity: Number,
        pressure: Number
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
    width: 450px;
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

</style>
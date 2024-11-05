<template>
    <div class="card">
        <div class="card_top">
            <div class="card__main-info">
                <svg xmlns="http://www.w3.org/2000/svg" height="48px" viewBox="0 -960 960 960" width="48px"
                    fill="#e8eaed">
                    <path
                        d="M450-770v-150h60v150h-60Zm256 106-42-42 106-107 42 43-106 106Zm64 214v-60h150v60H770ZM450-40v-150h60v150h-60ZM253-665 148-770l42-42 106 106-43 41Zm518 517L664-254l41-41 108 104-42 43ZM40-450v-60h150v60H40Zm151 302-43-42 105-105 22 20 22 21-106 106Zm289-92q-100 0-170-70t-70-170q0-100 70-170t170-70q100 0 170 70t70 170q0 100-70 170t-170 70Zm0-60q75 0 127.5-52.5T660-480q0-75-52.5-127.5T480-660q-75 0-127.5 52.5T300-480q0 75 52.5 127.5T480-300Zm0-180Z" />
                </svg>
                <span style="font-size: 32px;">{{ cloudness }}</span>
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
    width: fit-content;
    color: aliceblue;
    padding: 5px;
    font-family: Arial, Helvetica, sans-serif;
    transition: translate 0.5s;
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

.card:hover {
    translate: 0px -10px;
}
</style>
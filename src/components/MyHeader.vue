<template>
    <div class="header">
        <!-- <h1>Погода в {{ cities[selectedCity][City] }}</h1> -->
        <select class="header__select" name="" v-model="selectedCity" @change="getWeather">
            <option v-for="(v, k) in cities" :value="k" :key="k">{{ v["City"] }}</option>
        </select>
        <button @click="changeUnits">°{{ currentUnits }}</button>
    </div>

</template>

<script>
export default {
    data() {
        return {
            selectedCity: 0,
        }
    },
    props: {
        cities: JSON,
        currentUnits: String
    },
    methods: {
        changeUnits() {
            this.$parent.changeUnits()
        },
        getWeather() {
            this.$parent.getWeather()
        },
    }
}
</script>

<style scoped>
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.header__select {
    width: 450px;
}

.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1536px;
    margin-left: auto;
    margin-right: auto;
    padding-left: 0.5rem;
    padding-right: 0.5rem;
}

/* 2xl */
@media (max-width: 1536px) {
    .header__select {
        width: 350px;
    }
}

/* xl */
@media (max-width: 1280px) {

}

/* lg */
@media (max-width: 1024px) {

}

/* md */
@media (max-width: 768px) {

}

/* sm */
@media (max-width: 640px) {

}

/* xs */
@media (max-width: 475px) {
    .header__select {
        width: 300px;
    }
}
</style>
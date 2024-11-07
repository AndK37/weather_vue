<template>
    <div class="header">
        <!-- <h1>Погода в {{ cities[selectedCity][City] }}</h1> -->
        <select name="" v-model="selectedCity" @change="getWeather">
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

<style>
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>
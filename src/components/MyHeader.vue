<template>
    <div class="header">
        <div class="header__left">
            <select class="header__select" name="" v-model="selectedCity" @change="getWeather">
                <option v-for="(v, k) in cities" :value="k" :key="k">{{ v["City"] }}</option>
            </select>
            <button @click="setFeatured">☆</button>
        </div>
        <div class="header__right">
            <button @click="changeUnits">°{{ currentUnits }}</button>
        </div>
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
        setFeatured() {
            if (localStorage[String(this.selectedCity)] == 1) {
                localStorage.removeItem(String(this.selectedCity));
                console.log("rem");
            }
            else {
                localStorage[String(this.selectedCity)] = 1;
                console.log("set");
            }
        }
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
@media (max-width: 1280px) {}

/* lg */
@media (max-width: 1024px) {}

/* md */
@media (max-width: 768px) {}

/* sm */
@media (max-width: 640px) {}

/* xs */
@media (max-width: 475px) {
    .header__select {
        width: 300px;
    }
}
</style>
<template>
    <div class="list">
        <button class="list__item" v-for="n in feat" :key="n" :id="n" @click="sendFeature($event)">{{ this.$parent.cities[n]["City"] }} </button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            feat: Object.keys(localStorage),
        }
    },
    emits: ["sendFeature"],
    methods: {
        sendFeature(event) {
            this.$emit("sendSC", event.target.id)
        }
    },
    mounted() {
        if (Object.keys(localStorage) === undefined) {
            localStorage[0] = 1;
        }
    }
}
</script>

<style scoped>
.list {
    display: flex;
    flex-direction: column;
    width: 50%;
    gap: 10px;
}
.list__item {
    width: 100%;
}
</style>
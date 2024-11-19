<template>
    <div class="list" >
        <div class="list__item" :v-for="n in feature">
            <span>{{ n }}</span>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            feature: Object.keys(localStorage),
        }
    },
    methods: {

    },
    mounted() {
        console.log(this.feature);
    }
}
</script>
<style>

</style>

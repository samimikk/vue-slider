<template>
    <div class="slide" :id="'slide-' + id">
        <img v-bind:src="imagePath"  />
    </div>
</template>
<script>
    export default {
        name: "Slide",
        props: ['imagePath','id'],
        data() {
            return {}
        },
        computed: {},
        methods: {}
    }
</script>
<style lang="scss" scoped>
    .slide {
        width: 100%;
        img {
            display: block;
            max-width: 100%;
        }
    }
</style>
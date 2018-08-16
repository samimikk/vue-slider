<template>
    <div class="slider">
        <div class="slider__controls">
            <button class="slider__controller--next" v-on:click="showNextSlide()">Next slide</button>
            <button class="slider__controller--prev" v-on:click="showPrevSlide()">Previous slide</button>
        </div>
        <div class="slides__wrapper">
            <slide  v-for="(image, index) in images" v-bind:key="index" v-bind:id="index" v-bind:image-path="image" />
        </div>

    </div>
</template>
<script>
    import Slide from "@/components/Slide.vue";

    export default {
        name: "Slider",
        components: {
            Slide
        },
        data() {
            return {
                images: ['https://i.imgur.com/PLIYUfX.jpg','https://i.imgur.com/1bhGBhh.jpg','https://i.imgur.com/IesJxWz.jpg'],
                currentIndex: 0,
                offset: 0,
                stage: 0,
                wrapper: "",
                el: ""
            }
        },
        created: function() {
        },
        mounted: function() {

            this.init();

            this.$nextTick(function() {
                window.addEventListener('resize',this.resize);

                this.setBoundingBox();
            });
        },
        computed: {},
        methods: {
            resize() {
                this.init();
                this.setBoundingBox();
                this.stage = this.el.clientWidth;
                this.currentIndex = 0;
                this.offset = 0;
                this.wrapper.style.transform = 'translate(0px)';
            },
            buttonState() {
              var nextButton = document.querySelector('.slider__controller--next');
              var prevButton = document.querySelector('.slider__controller--prev');

                  if (this.currentIndex == this.images.length - 1) {
                      nextButton.disabled = true;
                  } else {
                      nextButton.disabled = false;
                  }
                  if (this.currentIndex == 0) {
                      prevButton.disabled = true;
                  } else {
                      prevButton.disabled = false;
                  }

              },
            init: function() {
                this.el = document.querySelector('.slider');
                this.wrapper = document.querySelector('.slides__wrapper');
                this.stage = this.el.clientWidth;
            },
            moveSlider: function() {
                this.wrapper.style.transform =  'translate(-'+this.offset+'px)';
            },
            setBoundingBox: function() {
                this.wrapper.style.width = this.el.clientWidth * this.images.length + 'px';
            },
            showNextSlide: function() {
                if (this.currentIndex < this.images.length - 1) {
                    this.offset = this.offset + this.stage;
                    this.moveSlider();
                    this.currentIndex++;
                    this.buttonState();
                }
            },
            showPrevSlide: function() {
                if (this.currentIndex > 0 ) {
                    this.offset = this.offset - this.stage;
                    this.moveSlider();
                    this.currentIndex--;
                    this.buttonState();
                }
            }
        },
        beforeDestroy: function () {
            window.removeEventListener('resize', this.resize);
        }
    }
</script>
<style scoped lang="scss">
    .slider {
        position: relative;
        width: 100%;
        overflow: hidden;
    }
    .slides__wrapper {
            display: flex;
            flex-direction: row;
            justify-content: flex-start;
            width: 100%;
            list-style-type: none;
            margin: 0;
            padding: 0;
            transition: transform .5s;
    }
    .slider__controls {

    }
</style>
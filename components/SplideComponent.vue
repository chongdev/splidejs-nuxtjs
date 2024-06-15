<template>
    <div class="container">
        <div ref="splide" class="splide">
            <div class="splide__track">
                <ul class="splide__list">
                    <li v-for="(item, index) in slides" :key="index" class="splide__slide">
                        <div class="card">
                            <div class="imageWraper">
                                <img :src="item" alt="" width="" height="" />
                            </div>
                        </div>
                    </li>
                </ul>
            </div>
        </div>

        <div class="custom-pagination">
            <button v-for="(slide, index) in slides" :key="index" :class="{ active: currentSlide === index }"
                @click="goToSlide(index)">
                {{ index + 1 }}
            </button>
        </div>

        <div class="custom-arrows">
            <button @click="goToSlide(currentSlide - 1)" :disabled="currentSlide === 0">Prev</button>
            <button @click="goToSlide(currentSlide + 1)" :disabled="currentSlide === slides.length - 1">Next</button>
        </div>
    </div>
</template>

<script>
import Splide from '@splidejs/splide';
import "@splidejs/splide/dist/css/splide.min.css";

export default {
    name: 'SplideComponent',

    data() {
        const items = [];

        for (let i = 0; i < 10; i++) {
            items.push(`https://picsum.photos/200/300?random=${i}`);
        }

        return {
            slides: items,
            splide: null,
            currentSlide: 0,
        }
    },

    mounted() {
        this.splide = new Splide(this.$refs.splide, {
            type: 'loop',
            perPage: 1,
            autoplay: true,
            interval: 3000,

            // heightRatio: 0.5,
            pagination: false,
            arrows: false,
        }).mount();

        this.splide.on('move', (newIndex) => {
            this.currentSlide = newIndex;
        });
    },
    methods: {
        goToSlide(index) {
            this.splide.go(index);
            this.currentSlide = index;
        },
    },
}
</script>

<style>
* {
    box-sizing: border-box;
}

html {
    font-size: 16px;
}

body {
    margin: 0;
    line-height: inherit;
}

.container {
    width: 100%;
    position: relative;
    margin: 0 auto;
    padding: 16px;
    overflow: hidden;
    background-color: #333;
}

.card {
    display: block;
    position: relative;
    background-color: #f2f2f2;
    aspect-ratio: 16 / 9;
    overflow: hidden;
}

.imageWraper {
    position: absolute;
    inset: 0;
    overflow: hidden;
}

.imageWraper img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}
</style>
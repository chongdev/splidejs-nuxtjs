<template>
    <div class="container">
        <div ref="splide" class="splide">
            <div class="splide__track">
                <ul class="splide__list">
                    <li v-for="(item, index) in items" :key="index" class="splide__slide">
                        <div class="card">
                            <div class="imageWraper">
                                <img :src="item" alt="" width="" height="" />
                            </div>
                        </div>
                    </li>
                </ul>
            </div>
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
            items,
        }
    },

    mounted() {
        new Splide(this.$refs.splide, {
            type: 'loop',
            perPage: 1,
            autoplay: true,
            interval: 3000,
        }).mount();
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
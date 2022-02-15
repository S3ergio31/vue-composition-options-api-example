<script setup>
import { reactive } from 'vue';
import CarouselComposition from './components/CarouselComposition.vue';
import CarouselOptions from './components/CarouselOptions.vue';

const state = reactive({
    active: {},
    items: [{ id: 1 }, { id: 2 }, { id: 3 }, { id: 4 }],
    carouseles: [
        {
            title: "Carousel with composition API",
            component: CarouselComposition
        },
        {
            title: "Carousel with options API",
            component: CarouselOptions
        }
    ]
});

const onChange = active => state.active = active;

</script>

<template>
    <template v-for="carousel in state.carouseles">
        <h1>{{ carousel.title }}</h1>
        <component 
            :is="carousel.component" 
            :items="state.items" 
            @change="onChange"
        >
            <p>{{ state.active.id }}</p>
        </component>
    </template>
</template>

<style scoped>
    p {
        background-color: royalblue;
        color: white;
        width: 100%;
        font-size: 40px;
        text-align: center;
    }
</style>
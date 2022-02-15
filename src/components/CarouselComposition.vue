<script setup>
import { computed, onMounted, ref } from 'vue';

const PREVIUS = -1;
const NEXT = 1;

const { items } = defineProps({
    items: Array
});

const emit = defineEmits(["change"]);

const index = ref(0);

const totalItems = computed(() => items.length);
const isBegin = computed(() => index.value === 0);
const isEnd = computed(() => index.value === totalItems.value - 1);
const shouldMove = computed(() => !isBegin.value || !isEnd.value);
const active = computed(() => items[index.value]);

onMounted(() => totalItems.value && emit('change', active.value));

const goTo = direction => {
    if (shouldMove.value) {
        index.value += direction;
        emit("change", active.value);
    }
}

const goToPrevious = () => goTo(PREVIUS);

const goToNext = () => goTo(NEXT);

</script>

<template>
    <div class="carousel">
        <button @click="goToPrevious" :disabled="isBegin">«</button>
        <slot />
        <button @click="goToNext" :disabled="isEnd">»</button>
    </div>
</template>

<style scoped>
.carousel {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>
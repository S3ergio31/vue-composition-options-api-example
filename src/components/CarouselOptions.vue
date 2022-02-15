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

<script>
    const PREVIUS = -1;
    const NEXT = 1;
    export default {
        props: {
            items: {
                type: Array,
                default: []
            }
        },
        data(){
            return {
                index: 0
            }
        },
        emits: ["change"],
        created(){
            this.totalItems && this.$emit('change', this.active);
        },
        computed: {
            totalItems(){
                return this.items.length;
            },
            isBegin(){
                return this.index === 0;
            },
            isEnd(){
                return this.index === this.totalItems -1;
            },
            shouldMove(){
                return !this.isBegin || !this.isEnd;
            },
            active(){
                return this.items[this.index];
            }
        },
        methods:{
            goTo(direction){
                if(this.shouldMove){
                    this.index += direction;
                    this.$emit("change", this.active);
                }
            },
            goToPrevious(){
                this.goTo(PREVIUS);
            },
            goToNext(){
                this.goTo(NEXT);
            }
        }
    }
</script>
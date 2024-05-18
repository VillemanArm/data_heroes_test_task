<script setup lang='ts'>
import { reactive, ref, computed, onMounted, onUpdated, watch } from 'vue'

const {setName, setStatus} = defineProps<{
    setName: Function;
    setStatus: Function;
}>();

const status = ref<string>()
const name = ref<string>()

const setFilterValues = () => {
    setStatus(status.value)
    setName(name.value)
}

</script>

<template>

    <form class="filter" @submit.prevent>
        <label for="status">Status:</label>
        <select id="status" v-model="status">
            <option value=""></option>
            <option value="Alive">Alive</option>
            <option value="Dead">Dead</option>
            <option value="unknown">Unknown</option>
        </select>
        
        <label for="name">Name: </label>
        <input id="name" type="text" v-model="name">
        
        <button type="button" @click="setFilterValues()">Search</button>
    </form>

</template>

<style scoped lang='sass'>
    @import '@/assets/styles/constants.sass'

    .filter
        display: flex
        gap: 10rem
        align-items: center

        font-size: 18rem

        &>select
            width: 100rem

        &>input
            padding: 0 4rem

        &>input, select
            height: 24rem

            font-size: 16rem

            border-radius: 4rem

        &>button
            padding: 3rem 8rem

            background-color: $secondary-font-color
            
            &:hover
                background-color: $orange
                color: $primary-font-color

    @media (max-width: 768px)
        .filter
            margin-bottom: 16rem
            display: grid
            grid-template-columns: 80rem 1fr
            gap: 8rem

            align-items: flex-start

            font-size: 16rem

            &>select
                width: 100%

            &>input
                padding: 0 4rem

            &>input, select
                height: 24rem

                font-size: 14rem

                border-radius: 4rem

            &>button
                padding: 3rem 8rem

                background-color: $secondary-font-color
                
                &:hover
                    background-color: $orange
                    color: $primary-font-color


            


</style>

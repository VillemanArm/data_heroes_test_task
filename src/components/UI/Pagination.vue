<script setup lang='ts'>
import { reactive, ref, computed, onMounted, onUpdated, watch } from 'vue'

defineProps<{
    setPage: Function;
    maxPage: number | null;
    currentPage: number;
}>();

</script>

<template>

   <div 
        v-if="maxPage > 1" 
        class="pagination"
    >
        <div 
            :class="{ 'pagination__arrow': true, 'pagination__arrow_active': currentPage !== 1 }"
            @click="setPage(currentPage - 1)"
        >
            <svg width="6" height="8" viewBox="0 0 6 8" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M4.66666 0.666626L1.33333 3.99996L4.66666 7.33329" stroke="evenodd" stroke-linecap="round"
                    stroke-linejoin="round" />
            </svg>
        </div>

        <div 
            v-for="page in maxPage" 
            :key="page"
        >
            <div 
                v-if="page === 1 || page === maxPage || (page <= currentPage + 2 && page >= currentPage - 2)"
                :class="{ 'pagination__button': true, 'pagination__button_active': page === currentPage }"
                @click="setPage(page)"
            >
                <div>{{ page }}</div>
            </div>
            <div 
                v-else-if="page === currentPage + 3 || page === currentPage - 3"
                class="pagination__skip"
            >
                <div>...</div>
            </div>
        </div>

        <div 
            :class="{ 'pagination__arrow': true, 'pagination__arrow_active': currentPage !== maxPage }"
            @click="setPage(currentPage + 1)"
        >
            <svg width="6" height="8" viewBox="0 0 6 8" fill="none" xmlns="http://www.w3.org/2000/svg" stroke="#8591AE">
                <path d="M1.33334 7.33337L4.66668 4.00004L1.33334 0.666707" stroke="evenodd" stroke-linecap="round"
                    stroke-linejoin="round" />
            </svg>
        </div>
    </div>

</template>

<style scoped lang='sass'>
    @import '@/assets/styles/constants.sass'

    .pagination
        display: flex
        align-items: center

        & svg
            stroke: $secondary-font-color

    .pagination__button
        width: 36rem 
        height: 36rem
        display: flex
        align-items: center
        justify-content: center

        border-radius: 12rem
        cursor: pointer
        color: $secondary-font-color

        &:hover
            color: $primary-font-color

    .pagination__button_active
        background-color: $background-color
        color: $primary-font-color

    .pagination__skip
        width: 36rem 
        height: 36rem
        display: flex
        align-items: center
        justify-content: center

        color: $secondary-font-color

    .pagination__arrow
        width: 20rem 
        height: 20rem
        display: flex
        align-items: center
        justify-content: center

    .pagination__arrow_active:hover
        background-color: $background-color
        cursor: pointer

        &>svg
            stroke: $primary-font-color


</style>

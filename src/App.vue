<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { reactive, ref, computed, onMounted, onUpdated, watch } from 'vue'
import axios from 'axios'

import CharacterCard from './components/CharacterCard.vue'

const serverURL: string = 'https://rickandmortyapi.com/graphql'

const charactersList = ref([])
const currentPage = ref<number>(1)

const getData = (query: string) => {
  axios.post(serverURL, {query})
    .then(function (response) {
      charactersList.value = JSON.parse(response.request.response).data.characters.results
    })
    .catch(function (error) {
      console.log(error);
    });
}

onMounted(() => {
  const starterQuery = `
      query {
        characters (page: ${currentPage.value}) {
          results {
            id
            image
            name
            status
            type
            location {
              name
            }
            episode {
              name
            }
          }
        }
      }
    `
  getData(starterQuery)
})

</script>

<template>

  <!-- <CharacterCard class="" v-for="character in charactersList" :key="character.id" :character="character"/> -->

</template>

<style scoped lang="sass">
  @import '@/assets/styles/constants.sass'

</style>./components/CharacterCard.vue

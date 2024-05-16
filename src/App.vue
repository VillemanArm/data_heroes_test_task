<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { reactive, ref, computed, onMounted, onUpdated, watch } from 'vue'
import axios from 'axios'

import Logo from './components/Logo.vue'
import CharacterCard from './components/CharacterCard.vue'

interface CharactersList {
  info: {
    pages: number
  },
  results: {
    id: number,
    image: string,
    name: string,
    status: 'Alive' | 'Dead' | 'unknown',
    species: string,
    location: {
      name: string
    },
    episode: {name: string}[]  
  }[]
}

export type { CharactersList }

const serverURL: string = 'https://rickandmortyapi.com/graphql'

const charactersList = ref<CharactersList>()
const currentPage = ref<number>(1)

const query = computed<string>(() => `
    query {
      characters (page: ${currentPage.value}) {
        info {
          pages
        }
        results {
          id
          image
          name
          status
          species
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
)

const getData = (query: string) => {
  axios.post(serverURL, {query})
    .then(function (response) {
      charactersList.value = JSON.parse(response.request.response).data.characters
    })
    .catch(function (error) {
      console.log(error);
    });
}

onMounted(() => {
  getData(query.value)
})

</script>

<template>
  <header>
    <div class="container characters-controls">
      <Logo/>
      <div class="characters-controls__pagination">

      </div>
      <div class="characters-controls__filter">

      </div>

    </div>

  </header>
  

  <div class="container characters-wrap">
    <CharacterCard class="" v-if="charactersList" v-for="character in charactersList.results" :key="character.id" :character="character"/>
  </div>
</template>

<style scoped lang="sass">
  @import '@/assets/styles/constants.sass'
  
  .container
    width: 1200rem
    margin: 0 auto

  header
    padding: 12rem 0

    background-color: $secondary-block-background-color

  .characters-wrap
    margin-top: 24rem
    display: grid
    grid-template-columns: repeat(2, 1fr)
    gap: 24rem

</style>

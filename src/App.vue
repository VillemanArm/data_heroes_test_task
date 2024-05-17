<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { reactive, ref, computed, onMounted, onUpdated, watch } from 'vue'
import axios from 'axios'

import Logo from '@/components/UI/Logo.vue'
import Pagination from '@/components/UI/Pagination.vue'
import Filter from '@/components/Filter.vue'
import CharacterCard from '@/components/CharacterCard.vue'

interface Character {
	id: number,
    image: string,
    name: string,
    status: 'Alive' | 'Dead' | 'unknown',
    species: string,
    location: {
      name: string
    },
    episode: {name: string}[]  
}

interface CharactersList {
  info: {
    pages: number
  },
  results: Character[]
}

export type { Character }

const serverURL: string = 'https://rickandmortyapi.com/graphql'

const charactersList = ref<CharactersList>()
const currentPage = ref<number>(1)
const status = ref<string>()
const name = ref<string>()

const setPage = (pageNumber: number) => {
  if (charactersList.value && (pageNumber > 0 && pageNumber <= charactersList.value?.info.pages)) {
    currentPage.value = pageNumber
  }
}

const setStatus = (newStatus: string) => {
    status.value = newStatus
}

const setName = (newName: string) => {
    name.value = newName
}

const query = computed<string>(() => `
    query {
      characters (
        page: ${currentPage.value}
        ${status.value || name.value ? `filter: {
          ${status.value ? `status: "${status.value}"` : ''}
          ${name.value ? `name: "${name.value}"` : ''}
        }` : ''}
        ) {
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

watch (query, () => {
  getData(query.value)
})

onMounted(() => {
  getData(query.value)
})

</script>

<template>
  <header>
    <div class="container">
      <Logo/>
    </div>
  </header>

    <div class="container characters-controls">
      <Pagination 
        v-if="charactersList" 
        :maxPage="charactersList.info.pages" 
        :setPage="setPage" 
        :currentPage="currentPage" 
      />
      <Filter
        :setStatus="setStatus"
        :setName="setName"
      />
    </div>
  
  <div class="container characters-wrap">
    <CharacterCard class="" v-if="charactersList" v-for="character in charactersList.results" :key="character.id" :character="character"/>
  </div>

  <div class="container">
    <div v-if="!charactersList?.results.length" class="characters-notification">
      <span class="characters-notification__content">There are no results for your request</span>
    </div>
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

  .characters-controls
    min-height: 60rem
    padding-top: 24rem
    display: flex
    justify-content: space-between
    align-items: center
    position: relative

  .filter
    position: absolute
    right: 0

  .characters-wrap
    margin-top: 24rem
    display: grid
    grid-template-columns: repeat(2, 1fr)
    gap: 24rem
  
  .characters-notification
    width: 100%
    height: 80vh
    position: relative

  .characters-notification__content  
    position: absolute
    top: 50%
    left: 50%
    transform: translate(-50%, 50%)
    
    font-size: 28rem



</style>

<script setup lang="ts">
import { reactive, ref, computed, onMounted, onUpdated, watch } from 'vue'
import type { Character } from '@/App.vue'

defineProps<{
	character: Character;
}>();

</script>

<template>

	<div class="character-card">
		<div class="character-card__img">
			<img :src="character.image" :alt="character.name" />
		</div>
		<div class="character-card__description">
			<div class="character-card__section">
				<h2>{{ character.name }}</h2>

				<span class="character-card__status">
					<span 
						:class="{
							'character-card__status-icon': true,
							'red': character.status === 'Dead',
							'green': character.status === 'Alive',
							'grey': character.status === 'unknown',
						}"
					></span> 
					<span>{{ character.status }} - {{ character.species }}</span>
				</span>
			</div>
			<div class="character-card__section">
				<span class="character-card__title">Last known location:</span><br>
				<span class="character-card__info">{{ character.location.name }}</span>
			</div>
			<div class="character-card__section">
				<span class="character-card__title">First seen in:</span><br>
				<span class="character-card__info">{{ character.episode[0].name }}</span>
			</div>
		</div>
	</div>

</template>

<style scoped lang="sass">
	@import '@/assets/styles/constants.sass'

	.character-card
		width: 100%
		height: 230rem
		display: flex

		border-radius: 10rem
		background-color: $block-background-color

	.character-card__img
		width: 220rem
		height: 100%

		&>img
			object-fit: fill
			border-radius: 10rem 0 0 10rem


	.character-card__description
		display: grid
		padding: 12rem
		align-content: space-between

	.character-card__status
		display: flex
		align-items: top
		margin-top: 4rem

		font-weight: 500
		
	.character-card__status-icon
		width: 9rem
		height: 9rem
		display: inline-block
		margin-right: 7rem
		
		border-radius: 50%
		background-color: red

	.red
		background-color: $red

	.green
		background-color: $green

	.grey
		background-color: $secondary-font-color

	.character-card__title
		display: inline-block
		margin-bottom: 10rem

		color: $secondary-font-color

	.character-card__info
		font-size: 18rem
		  
</style>






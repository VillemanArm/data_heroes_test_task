<script setup lang="ts">
import { reactive, ref, computed, onMounted, onUpdated, watch } from 'vue'

defineProps<{
	character: object;
}>();

</script>

<template>

	<div class="character-card">
		<div class="character-card__img">
			<img src="https://rickandmortyapi.com/api/character/avatar/75.jpeg" alt="Courier Flap">
		</div>
		<div class="character-card__description">
			<div class="character-card__section">
				<h2>Courier Flap</h2>

				<span class="character-card__status">
					<span class="character-card__status-icon"></span> 
					<span>Alive - Alien</span>
				</span>
			</div>
			<div class="character-card__section">
				<span class="character-card__title">Last known location:</span><br>
				<span class="character-card__info">Planet Squanch</span>
			</div>
			<div class="character-card__section">
				<span class="character-card__title">First seen in:</span><br>
				<span class="character-card__info">The Wedding Squanchers</span>
			</div>
		</div>
	</div>

</template>

<style scoped lang="sass">
	@import '@/assets/styles/constants.sass'

	.character-card
		width: 475rem
		height: 200rem
		display: flex

		border-radius: 16rem
		background-color: $block-background-color

	.character-card__img
		width: 200rem
		height: 100%

		&>img
			object-fit: fill
			border-radius: 16rem 0 0 16rem


	.character-card__description
		display: grid
		padding: 12rem
		align-content: space-between


		// border-left-radius: 8rem

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

	.character-card__title
		display: inline-block
		margin-bottom: 9rem

		font-size: 15rem

		color: $secondary-font-color

	.character-card__info
		font-size: 16rem
		
    
</style>






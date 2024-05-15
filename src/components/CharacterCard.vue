<script setup lang="ts">
import { reactive, ref, computed, onMounted, onUpdated, watch } from 'vue'

defineProps<{
	character: object;
}>();

</script>

<template>

	<article class="characterCard__Wrapper-sc-1ejywvi-0 bEklxv">
		<div class="characterCard__ImgWrapper-sc-1ejywvi-1 fkUcVI">
			<img src="https://rickandmortyapi.com/api/character/avatar/75.jpeg" alt="Courier Flap">
		</div>
		<div class="characterCard__ContentWrapper-sc-1ejywvi-2 isMAic">
			<div class="section">
				<a href="https://rickandmortyapi.com/api/character/75" rel="noopener noreferrer" target="_blank" class="externalLink__ExternalLink-sc-1lixk38-0 ffGNdR">
					<h2>Courier Flap</h2>
				</a>
				<span class="status">
				<span class="status__icon">
				</span> Alive - Alien</span>
			</div>
			<div class="section">
				<span class="text-gray">Last known location:</span>
				<a href="https://rickandmortyapi.com/api/location/35" rel="noopener noreferrer" target="_blank" class="externalLink__ExternalLink-sc-1lixk38-0 ffGNdR">Planet Squanch</a>
			</div>
			<div class="section">
				<span class="text-gray">First seen in:</span>
				<a href="https://rickandmortyapi.com/api/episode/21" rel="noopener noreferrer" target="_blank" class="externalLink__ExternalLink-sc-1lixk38-0 ffGNdR">The Wedding Squanchers</a>
			</div>
		</div>
	</article>

</template>

<style scoped lang="sass">
	@import '@/assets/styles/constants.sass'


    
</style>


	// -webkit-text-size-adjust: 100%;
    // font: 112.5%/1.625 -apple-system,'BlinkMacSystemFont','Segoe UI','Roboto','Helvetica','Arial',//sans-serif,'Apple Color Emoji','Segoe UI Emoji','Segoe UI Symbol';
    // color: hsla(0,0%,0%,0.8);
    // font-family: -apple-system,'BlinkMacSystemFont','Segoe UI','Roboto','Helvetica','Arial',sans-serif,'Apple Color Emoji','Segoe UI Emoji','Segoe UI Symbol';
    // font-weight: normal;
    // word-wrap: break-word;
    // font-kerning: normal;
    // font-feature-settings: "kern", "liga", "clig", "calt";
    // font-variant-ligatures: none;
    // text-rendering: optimizelegibility;
    // -webkit-font-smoothing: antialiased;
    // text-decoration-skip-ink: auto;
    // box-sizing: inherit;
    // width: 600px;
    // height: 220px;



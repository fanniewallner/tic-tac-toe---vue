<script setup lang="ts">
import ChoosePlayers from './components/ChoosePlayers.vue';
import GridComponent from './components/GridComponent.vue'
import Game from './components/Game.vue';
import { ref } from 'vue';

let show = ref(true)

function toggleShow() {
  show.value = !show.value
}



</script>

<template>
  <h1>Tic-Tac-Toe</h1>
  <ChoosePlayers v-if="show" @start-game="toggleShow"></ChoosePlayers>
  <GridComponent v-else></GridComponent>
  <Game></Game>
</template>

<style scoped></style>

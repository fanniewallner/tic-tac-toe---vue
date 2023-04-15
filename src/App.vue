<script setup lang="ts">
import ChoosePlayers from './components/ChoosePlayers.vue';
import GridComponent from './components/GridComponent.vue'
import ScoreBoard from './components/ScoreBoard.vue';
import { Player } from './models/Player';
import { ref } from 'vue';

//let currentPlayers = ref<Player[]>(JSON.parse(localStorage.getItem("playerStats") || "[]"))
let currentPlayers = ref<Player[]>([])

const addPlayer = (usernameX: string, usernameO: string) => {
  currentPlayers.value = [
    new Player(usernameX, 0),
    new Player(usernameO, 0)
  ]
  show.value = false
}

const showScore = () => {
  showScoreToggle.value = true
  show.value
  console.log(showScoreToggle.value)
  console.log("Funktionen körs")
}

let showScoreToggle = ref(false)
let show = ref(true)

</script>

<template>
  <div class="container">
    <h1>Tic-Tac-Toe</h1>
    <div id="body">
      <ChoosePlayers v-if="show" @add-player="addPlayer">
      </ChoosePlayers>
      <GridComponent v-else v-if="!showScoreToggle" :players="currentPlayers" @show-score="showScore">
      </GridComponent>
      <ScoreBoard v-if="showScoreToggle" :players="currentPlayers"></ScoreBoard>
    </div>
  </div>
</template>

<style scoped></style>

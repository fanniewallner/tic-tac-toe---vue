<script setup lang="ts">
import ChoosePlayers from './components/ChoosePlayers.vue';
import GridComponent from './components/GridComponent.vue'
import ScoreBoard from './components/ScoreBoard.vue';
import { Player } from './models/Player';
import { ref } from 'vue';

const newPlayers = () => {
  show.value = true
  localStorage.clear()
}

const resumeGame = () => {
  showScoreToggle.value = false
}

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
      <ChoosePlayers class="choose-players" v-if="show" @add-player="addPlayer">
      </ChoosePlayers>
      <GridComponent v-else v-if="!showScoreToggle" :players="currentPlayers" @show-score="showScore"
        @new-players="newPlayers">
      </GridComponent>
      <ScoreBoard class="score-board" v-if="showScoreToggle" :players="currentPlayers" @resume-game="resumeGame">
      </ScoreBoard>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
}

h1 {
  font-size: 2em;
  margin-top: 0;
  margin-bottom: 1em;
}

#body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
}

.choose-players {
  margin-bottom: 1em;
  text-align: center;
}

.grid-component {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(3, 1fr);
  gap: 1em;
}

.score-board {
  margin-top: 1em;
}
</style>
<script setup lang="ts">
import ChoosePlayers from './components/ChoosePlayers.vue';
import GridComponent from './components/GridComponent.vue'
import ScoreBoard from './components/ScoreBoard.vue';
import { Player } from './models/Player';
import { ref } from 'vue';


let currentPlayers = ref<Player[]>([])

const addPlayer = (usernameX: string, usernameO: string) => {
  currentPlayers.value = [
    new Player(usernameX, 0),
    new Player(usernameO, 0)
  ]
  show.value = false
  console.log(currentPlayers.value)
}

let show = ref(true)

</script>

<template>
  <h1>Tic-Tac-Toe</h1>
  <div id="body">
    <ChoosePlayers v-if="show" @add-player="addPlayer">
    </ChoosePlayers>
    <GridComponent v-else :players="currentPlayers">
      <ScoreBoard></ScoreBoard>
    </GridComponent>
  </div>
</template>

<style scoped></style>

<script setup lang="ts">
import { Player } from '../models/Player';
interface IShowScoreProps {
    players: Player[]
}

const scoreProps = defineProps<IShowScoreProps>()
console.log(scoreProps.players)

const stats = <Player[]>(JSON.parse(localStorage.getItem("playerStats") || "[]"))
</script>


<template>
    <h2>Scores</h2>
    <div>
        <p>{{ scoreProps.players[0].username }}</p>
        <p>{{ scoreProps.players[0].score }}</p>
    </div>
    <div>
        <p>{{ scoreProps.players[1].username }}</p>
        <p>{{ scoreProps.players[1].score }}</p>
    </div>
</template>

<style></style>
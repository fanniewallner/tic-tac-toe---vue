<script setup lang="ts">
import { Player } from '../models/Player';
interface IShowScoreProps {
    players: Player[]
}

const scoreProps = defineProps<IShowScoreProps>()
console.log(scoreProps.players)

defineEmits(["resumeGame"])

//const stats = <Player[]>(JSON.parse(localStorage.getItem("playerStats") || "[]"))
</script>


<template>
    <div class="scoreboard">
        <div>

        </div>
        <h2>Scores</h2>
        <div>
            <p> Player: {{ scoreProps.players[0].username }}</p>
            <p> Won games: {{ scoreProps.players[0].score }}</p>
        </div>
        <div>
            <p> Player: {{ scoreProps.players[1].username }}</p>
            <p> Won games: {{ scoreProps.players[1].score }}</p>
        </div>
        <button @click="$emit('resumeGame')"> Resume game </button>
    </div>
</template>

<style scoped>
.scoreboard {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-top: 2rem;
    width: 400px;
    padding: 32px;
    background-color: #f2f2f2;
    border-radius: 8px;
}

h2 {
    font-size: 2rem;
    text-align: center;
    margin-bottom: 1rem;
}

div {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 80%;
    margin-bottom: 1rem;
}

p {
    font-size: 1.2rem;
    font-weight: bold;
    margin-right: 1rem;
}

button {
    background-color: #5e83a1;
    border: none;
    color: white;
    padding: 1rem 2rem;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 1.2rem;
    margin-top: 1rem;
    cursor: pointer;
}
</style>
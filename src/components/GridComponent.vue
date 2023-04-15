<script setup lang="ts">
import { computed } from '@vue/reactivity';
import { ref } from 'vue';
import { Player } from '../models/Player';

defineEmits(["showScore"]);

let currentPlayers = ref<Player[]>(JSON.parse(localStorage.getItem("playerStats") || "[]"))

function saveStats(currentPlayers: Player[]) {
    localStorage.setItem("playerStats", JSON.stringify(currentPlayers))
}

interface IShowPlayerProps {
    players: Player[]
}

const props = defineProps<IShowPlayerProps>()
const player = ref('X')
const currentPlayer = ref<Player>(props.players[0])

function toggleCurrentPlayer() {
    currentPlayer.value = currentPlayer.value === props.players[0] ? props.players[1] : props.players[0]
}

const cells = ref([
    ['', '', ''],
    ['', '', ''],
    ['', '', ''],
])

const winner = computed(() => isWinner(cells.value.flat()))

const isWinner = (cells: string[]) => {
    const possibleWins = [[0, 1, 2], [3, 4, 5], [6, 7, 8], [0, 3, 6], [1, 4, 7], [2, 5, 8], [0, 4, 8], [2, 4, 6]]

    for (let i = 0; i < possibleWins.length; i++) {
        const [a, b, c] = possibleWins[i]
        if (cells[a] && cells[a] === cells[b] && cells[a] === cells[c]) {
            return cells[a]
        }
    }
    return null
}


const playerMove = (x: number, y: number) => {
    if (winner.value || cells.value[x][y]) return
    cells.value[x][y] = player.value
    player.value = player.value === 'O' ? 'X' : 'O'
    if (winner.value) {
        currentPlayer.value.score += 1

        let foundPlayer = false
        for (let i = 0; i < currentPlayers.value.length; i++) {
            if (currentPlayers.value[i].username === currentPlayer.value.username) {
                currentPlayers.value[i].score = currentPlayer.value.score
                foundPlayer = true
            }
        }
        if (!foundPlayer) {
            currentPlayers.value.push(currentPlayer.value)
        }
        saveStats(currentPlayers.value)
        return
    }
    toggleCurrentPlayer()

}

function handleMove(event: MouseEvent) {
    const cellId = (event.target as HTMLElement).id;
    if (winner.value) return
    const [rowIndex, cellIndex] = cellId.split('-')
    playerMove(Number(rowIndex), Number(cellIndex))
}

function restartGrid() {
    cells.value = [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
    ];
    player.value = player.value === 'O' ? 'X' : 'O'
}
</script>


<template>
    <div id="grid-template">
        <p v-if="!winner"> {{ currentPlayer.username }}'s turn</p>
        <div class="row" v-for="(row, rowIndex) in cells" :key="rowIndex">
            <div class="cell" v-for="(cell, cellIndex) in row" :key="cellIndex" :id="`${rowIndex}-${cellIndex}`"
                :class="{ 'cell-x': cell === 'X', 'cell-o': cell === 'O' }" @click="handleMove">

            </div>
        </div>
    </div>
    <button @click="restartGrid">Restart game</button>
    <button @click="$emit('showScore')">Show score</button>
    <button>New players</button>
    <p class="winner" v-if="winner">Congratulations!! The winner is {{ currentPlayer.username }}</p>
</template>

<style scoped>
.grid-template {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
}

.row {
    display: flex;
}

.cell {
    border: 2px solid black;
    background-color: white;
    padding: 10px;
    height: 70px;
    width: 70px;
    display: inline-block;
}

.cell:hover {
    background-color: rgba(22, 22, 22, 0.079);
}

.cell-x::before {
    content: "X";
    font-size: 40px;
    font-weight: bolder;
}

.cell-o::before {
    content: "O";
    font-size: 40px;
    font-weight: bolder;
}

.winner {
    font-size: 20px;
    font-weight: bolder;
}
</style>
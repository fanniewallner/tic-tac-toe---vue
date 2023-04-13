<script setup lang="ts">
import { computed } from '@vue/reactivity';
import { ref } from 'vue';
import { Player } from '../models/Player';


const player = ref('X' ? 'O' : 'X')

const cells = ref([
    ['', '', ''],
    ['', '', ''],
    ['', '', ''],
])

const isWinner = (cells: string[]) => {
    const lines = [[0, 1, 2], [3, 4, 5], [6, 7, 8], [0, 3, 6], [1, 4, 7], [2, 5, 8], [0, 4, 8], [2, 4, 6]]

    for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i]
        if (cells[a] && cells[a] === cells[b] && cells[a] === cells[c]) {
            return cells[a]
        }
    }
    return null
}

const winner = computed(() => isWinner(cells.value.flat()))

const move = (x: number, y: number) => {
    if (winner.value) return
    cells.value[x][y] = player.value
    player.value = player.value === 'O' ? 'X' : 'O'
}

function handleMove(event: MouseEvent) {
    const cellId = (event.target as HTMLElement).id;
    if (winner.value) return
    const [rowIndex, cellIndex] = cellId.split('-')
    move(Number(rowIndex), Number(cellIndex))
}

function restartGrid() {
    cells.value = [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
    ];
}
</script>

<template>
    <div id="grid-template">
        <p v-if="!winner"> Player {{ player }}'s turn</p>
        <div class="row" v-for="(row, rowIndex) in cells" :key="rowIndex">
            <div class="cell" v-for="(cell, cellIndex) in row" :key="cellIndex" :id="`${rowIndex}-${cellIndex}`"
                :class="{ 'cell-x': cell === 'X', 'cell-o': cell === 'O' }" @click="handleMove">
            </div>
        </div>
    </div>
    <button @click="restartGrid">Restart game</button>
    <p class="winner" v-if="winner">Congratulations!! The winner is {{ winner }}</p>
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
    border: 1px solid black;
    background-color: white;
    padding: 10px;
    height: 70px;
    width: 70px;
    display: inline-block;
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
}</style>
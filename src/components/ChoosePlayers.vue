<script setup lang="ts">
import { ref } from 'vue';

//const player = ref<Player[]>
const usernameX = ref("")
const usernameO = ref("")

const emit = defineEmits(["startGame"])


</script>

<template>
    <p>Spelare X: {{ usernameX }}</p>
    <form @submit.prevent="() => $emit('addPlayer', usernameX)">
        <input type="text" placeholder="Enter name" v-model="usernameX">
        <p>Spelare O: {{ usernameO }}</p>
        <input type="text" placeholder="Enter name" v-model="usernameO">
        <button class="playBtn" @click="() => $emit('startGame', usernameX, usernameO)">Play</button>
    </form>
</template>

<style scoped>
.playBtn {
    display: block;
    display: flex;
    justify-content: center;
}
</style>
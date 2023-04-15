<script setup lang="ts">
import { ref } from 'vue';
import { Player } from '../models/Player';

const usernameX = ref("")
const usernameO = ref("")

defineEmits(["start-game", "add-player"]);

</script>

<template>
    <p>Spelare X: {{ usernameX }}</p>
    <form @submit.prevent="$emit('add-player', usernameX, usernameO)">
        <input type="text" placeholder="Enter name" v-model="usernameX">
        <p>Spelare O: {{ usernameO }}</p>
        <input type="text" placeholder="Enter name" v-model="usernameO">
        <button class="playBtn">Play</button>
    </form>
</template>

<style scoped>
.playBtn {
    display: block;
}
</style>
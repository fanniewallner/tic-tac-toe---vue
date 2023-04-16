<script setup lang="ts">
import { ref } from 'vue';

const usernameX = ref("")
const usernameO = ref("")

defineEmits(["start-game", "add-player"]);

</script>

<template>
    <div class="container">
        <div class="formWrapper">
            <p class="playerName">Spelare X: {{ usernameX }}</p>
            <p class="playerName">Spelare O: {{ usernameO }}</p>
            <form @submit.prevent="$emit('add-player', usernameX, usernameO)">
                <div class="inputWrapper">
                    <input class="input" type="text" placeholder="Enter name" v-model="usernameX">
                </div>
                <div class="inputWrapper">
                    <input class="input" type="text" placeholder="Enter name" v-model="usernameO">
                </div>
                <button class="playBtn">Play</button>
            </form>
        </div>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    justify-content: center;
    align-items: center;

}

.formWrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 400px;
    padding: 32px;
    background-color: #f2f2f2;
    border-radius: 8px;
}

.playerName {
    margin-bottom: 8px;
    font-size: 16px;
    font-weight: bolder;
    text-align: center;
}

.form {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
}

.inputWrapper {
    margin-bottom: 16px;
    width: 100%;
}

.input {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 16px;
}

.playBtn {
    margin-top: 16px;
    padding: 8px 16px;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    font-weight: bold;
    background-color: #5e83a1;
    color: #fff;
    cursor: pointer;
}
</style>
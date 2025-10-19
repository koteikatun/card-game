<script setup>
import { onMounted, ref, provide } from 'vue';
import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import Headers from "./components/Headers.vue";

const API_ENDPOINT = "http://localhost:8080/api/random-words";

let data = ref();
let start = ref(false);
let score = ref(100);

async function getRandomWords() {
  const res = await fetch(API_ENDPOINT);
  data.value = await res.json();
}

function changeStateGame(startGame) {
  start.value = startGame;
}

function refreshGame() {
  data.value = [];
  getRandomWords();
}

onMounted(() => {
  getRandomWords();
})

provide('score', score);

const handleScore = (status) => {
  if (status === 'Да') {
    score.value = score.value + 10;
  } else {
    score.value = score.value - 4;
  }
}
</script>

<template>
  <div class="main">
    <Headers />
    <div v-if="!start" class="buttons">
      <Button mode="start" @action="changeStateGame" />
    </div>
    <div v-else class="display-card">
      <div v-for="(word, index) in data" :key="index">
        <Card :content-card-foreign="word.word" :number-card="index" :content-card-translate="word.translation"
          @set-status="handleScore" />
      </div>
      <Button mode="restart" class="button-restart" @click="refreshGame" />
    </div>
  </div>
</template>

<style scoped>
.main {
  height: 100vh;
}

.buttons {
  display: flex;
  justify-content: center;
}

.display-card {
  margin-top: 2%;
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: center;
}

.button-restart {
  margin-top: 101px;
  margin-bottom: 65px;
}
</style>

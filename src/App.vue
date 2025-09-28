<script setup>
import { onMounted, ref } from 'vue';
import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import Headers from "./components/Headers.vue";

const API_ENDPOINT = "http://localhost:8080/api/random-words";

let data = ref();
let start = ref(false);

async function getRandomWords() {
  const res = await fetch(API_ENDPOINT);
  data.value = await res.json();
}

function changeStateGame(startGame) {
  start.value = startGame;
}

onMounted(() => {
  getRandomWords();
})

</script>

<template>
  <div class="main">
    <Headers />
    <div v-if="!start" class="buttons">
      <Button @start-game="changeStateGame" />
    </div>
    <div v-else class="display-card">
      <div v-for="(word, index) in data" :key="index">
        <Card :content-card-foreign="word.word" :number-card="index" :content-card-translate="word.translation" />
      </div>
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
</style>

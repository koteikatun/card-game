<script setup>
import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import Headers from "./components/Headers.vue";

const cards = [
  {
    contentCardForeign: "Fox",
    contentCardTranslate: "Лиса",
    numberCard: "01",
  },
  {
    contentCardForeign: "Flowers",
    contentCardTranslate: "Цветы",
    numberCard: "02",
  },
];
</script>

<template>
  <div class="main">
    <Headers />
    <div class="buttons">
      <Button />
    </div>
    <div class="displaycard">
      <div v-for="(card, index) in cards" :key="index">
        <Card v-bind="card" />
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
.displaycard {
  margin-top: 2%;
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: center;
}
</style>

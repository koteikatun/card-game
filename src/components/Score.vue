<script setup>
import { inject } from "vue";
import Heart from "../icons/Heart.vue";

const score = inject('score');
</script>

<template>
  <div class="headers-hearts">
    <div class="number">{{ score }}</div>
    <Heart />
  </div>
</template>

<style scoped>
.headers-hearts {
  margin-right: 62px;
  margin-top: 37px;
  width: 110px;
  height: 48px;
  border-radius: 36px;
  box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.15);
  background: #cce8ff;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.number {
  font-family: var(--font);
  font-weight: 700;
  font-size: 16px;
  line-height: 150%;
  text-align: center;
  color: #008bfe;
}
</style>

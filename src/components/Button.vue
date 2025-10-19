<script setup>
import { computed } from 'vue'

const props = defineProps({
  mode: {
    type: String,
    default: 'start', // 'start' | 'restart'
    validator: (value) => ['start', 'restart'].includes(value)
  }
})

const emit = defineEmits(['action'])

const buttonText = computed(() =>
  props.mode === 'start' ? 'Начать игру' : 'Начать заново'
)

const actionType = computed(() =>
  props.mode === 'start' ? 'start' : 'restart'
)
</script>

<template>
  <button class="btn" @click="$emit('action', actionType)">{{ buttonText }}</button>
</template>

<style scoped>
.btn {
  border: none;
  border-radius: 100px;
  /* padding: 16px 10px; */
  font-weight: 400;
  font-size: 24px;
  line-height: 150%;
  /* text-align: center; */
  color: var(--color-primary);
  font-family: var(--font);
  background: var(--color-bg-main);
  width: 335px;
  height: 68px;
  /* margin: 686px 531px; */
  cursor: pointer;
}
</style>

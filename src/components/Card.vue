<script setup>
import { ref } from "vue";
import Fail from "../icons/Fail.vue";
import Success from "../icons/Success.vue";

const props = defineProps({
  numberCard: {
    type: String,
  },
  contentCardForeign: {
    type: String,
  },
  contentCardTranslate: {
    type: String,
  },
});

let isFlipped = ref(false);
let status = ref("");

const emit = defineEmits({
  viewTranslate(payload) {
    return payload;
  },
  setStatus(payload) {
    return payload;
  },
});

function viewTranslate() {
  isFlipped.value = true;
  emit("viewTranslate", true);
}

function changeStat(setStatus) {
  if (setStatus) {
    status.value = "Да";
  } else {
    status.value = "Нет";
  }
  emit("setStatus", status.value);
}

</script>
<template>
  <div class="card">
    <div class="card-number">{{ props.numberCard }}</div>
    <div class="border-card">
      <div v-if="!isFlipped">
        <div class="card-content">{{ props.contentCardForeign }}</div>
        <button class="flip-button" @click="viewTranslate">ПЕРЕВЕРНУТЬ</button>
      </div>
      <div v-else>
        <div v-if="status === 'Да'" class="resultStatus">
          <Success :width="36" :height="36" />
        </div>
        <div v-else-if="status === ''" class="resultStatus">
          <div></div>
        </div>
        <div v-else class="resultStatus">
          <Fail :width="36" :height="36" />
        </div>
        <div class="card-content">{{ props.contentCardTranslate }}</div>
        <div v-if="status === ''" class="icons-variable">
          <Fail class="button-result" @click="changeStat(false)" />
          <Success class="button-result" @click="changeStat(true)" />
        </div>
        <div v-else class="finally">
          ЗАВЕРШЕНО
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.finally {
  border: none;
  width: 97px;
  height: 18px;
  background: var(--color-primary);
  position: absolute;
  bottom: 19px;
  left: 80px;
  font-family: var(--font);
  font-weight: 700;
  font-size: 12px;
  line-height: 150%;
  letter-spacing: 0.12em;
  color: var(--color-font);
  text-align: center;
  align-items: center;
}

.card {
  border-radius: 16px;
  width: 250px;
  height: 376px;
  box-shadow: 0 0 16px 0 rgba(0, 0, 0, 0.1);
  background: var(--color-primary);
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.border-card {
  border: 1px solid #cce8ff;
  border-radius: 12px;
  width: 212px;
  height: 320px;
  margin: 28px 19px;
}

.card-number {
  position: absolute;
  top: 20px;
  left: 35px;
  font-size: 14px;
  font-family: var(--font);
  font-weight: 400;
  color: var(--color-card);
  background: var(--color-primary);
}

.card-content {
  font-family: var(--font-family);
  font-weight: 400;
  font-size: 18px;
  text-align: center;
  color: var(--color-card);
  align-items: center;
  width: 180px;
  height: 21px;
  margin: 149px 16px;
}

.flip-button {
  border: none;
  width: 97px;
  height: 18px;
  background: var(--color-primary);
  position: absolute;
  bottom: 19px;
  left: 80px;
  font-family: var(--font);
  font-weight: 700;
  font-size: 12px;
  line-height: 150%;
  letter-spacing: 0.12em;
  color: var(--color-font);
  cursor: pointer;
}

.icons-variable {
  display: flex;
  justify-content: center;
  position: absolute;
  bottom: 19px;
  left: 80px;
  gap: 32px;
  background: var(--color-primary);
  width: 97px;
  height: 18px;
}

.button-result {
  cursor: pointer;
}

.resultStatus {
  display: flex;
  justify-content: center;
  position: absolute;
  top: 15px;
  left: 109px;
  width: 36px;
  height: 36px;
}
</style>

<script setup lang="ts">
import { ref } from 'vue';
import type { TStatus } from '@/types/TStatus';

interface Props {
  word: string;
}

defineProps<Props>()

const gameStatus = ref<TStatus | null>(null);
const isVisible = ref(false);

const open = (status: TStatus) => {
  gameStatus.value = status
  isVisible.value = true;
};
const close = () => {
  isVisible.value = false;
};
defineExpose({
  open,
  close,
});

const emit = defineEmits<{
  (e: 'restart'): void
}>()
</script>
<template lang="">
  <div v-if="isVisible" class="popup-container">
    <div class="popup">
      <h2 v-if="gameStatus === 'win'">Поздравляю, вы победили! 😃</h2>
      <template v-else>
        <h2>Вы проиграли. 😕</h2>
        <h3>...имя: {{word}}</h3>
      </template>

      <button @click="emit('restart')">Сыграть еще раз</button>
    </div>
  </div>
</template>

<style lang=""></style>

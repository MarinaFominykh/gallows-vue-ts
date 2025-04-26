<script setup lang="ts">
import {
  computed,
  defineComponent,
  ref,
  watch,
  onMounted,
  onUnmounted,
} from 'vue';
import GameHeader from './components/GameHeader.vue';
import GameFigure from './components/GameFigure.vue';
import GameWrongLetters from './components/GameWrongLetters.vue';
import GameWord from './components/GameWord.vue';
import GamePopup from './components/GamePopup.vue';
import GameNotification from './components/GameNotification.vue';
import axios from 'axios';
import { getRandomName } from './api/getRandomName';
import { useRandomWord } from './composables/useRandomWord';
import { useLetters } from './composables/useLetters';
import { useNotification } from './composables/useNotification';

const { word, getRandomWord } = useRandomWord();
const {
  letters,
  correctLetters,
  wrongLetters,
  isLose,
  isWin,
  addLetter,
  resetLetters,
} = useLetters(word);
const { notification, showNotification } = useNotification();

const popup = ref<InstanceType<typeof GamePopup> | null>(null);
const restart = async () => {
  await getRandomWord();
  resetLetters();
  //letters.value = [];
  popup.value?.close();
};

watch(wrongLetters, () => {
  if (isLose.value) {
    popup.value?.open('lose');
  }
});
watch(correctLetters, () => {
  if (isWin.value) {
    popup.value?.open('win');
  }
});
notification.value?.open();

const handleKeydown = ({ key }: KeyboardEvent) => {
  if (isWin.value || isLose.value) {
    return;
  }

  if (letters.value.includes(key.toLocaleLowerCase())) {
    showNotification();
    return;
  }
  addLetter(key);
};
window.addEventListener('keydown', handleKeydown);
</script>
<template lang="">
  <GameHeader />
  
  <div class="game-container">
    <GameFigure :wrong-letters-count="wrongLetters.length" />
    <GameWrongLetters :wrong-letters="wrongLetters" />
    <GameWord :word="word" :correct-letters="correctLetters" />
    <GamePopup ref="popup" @restart="restart" :word="word" />
  </div>
  <GameNotification ref="notification" />
</template>

<style lang=""></style>

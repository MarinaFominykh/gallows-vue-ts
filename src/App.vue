<script setup lang="ts">
import { computed, defineComponent, ref } from 'vue';
import GameHeader from './components/GameHeader.vue';
import GameFigure from './components/GameFigure.vue';
import GameWrongLetters from './components/GameWrongLetters.vue';
import GameWord from './components/GameWord.vue';
import GamePopup from './components/GamePopup.vue';
import GameNotification from './components/GameNotification.vue';

const word = ref("Василий")
const letters = ref<string[]>([])
const correctLetters = computed(() =>
  letters.value.filter(letter =>
    word.value.toLowerCase().includes(letter.toLowerCase())
  )
)
window.addEventListener('keydown', ({ key }) => {
  if (/[а-яА-ЯёЁ]/.test(key)) {
    letters.value.push(key.toLowerCase())
  }
})
</script>
<template lang="">
  <GameHeader />
  {{word}}
  {{letters}}
  {{correctLetters}}
  <div class="game-container">
    <GameFigure />
    <GameWrongLetters />
    <GameWord :word="word" :correct-letters="correctLetters"/>
    <GamePopup v-if="false" />
  </div>
  <GameNotification />
</template>


<style lang=""></style>




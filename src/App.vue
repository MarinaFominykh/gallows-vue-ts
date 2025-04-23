<template lang="">
  <GameHeader />
  <div class="game-container">
    <GameFigure />
    <GameWrongLetters />
    <GameWord />
    <GamePopup />
  </div>
  <GameNotification />
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import GameHeader from './components/GameHeader.vue';
import GameFigure from './components/GameFigure.vue';
import GameWrongLetters from './components/GameWrongLetters.vue';
import GameWord from './components/GameWord.vue';
import GamePopup from './components/GamePopup.vue';
import GameNotification from './components/GameNotification.vue';

export default defineComponent({
  components: {
    GameHeader,
    GameFigure,
    GameWrongLetters,
    GameWord,
    GamePopup,
    GameNotification,
  },
});
</script>

<style lang=""></style>

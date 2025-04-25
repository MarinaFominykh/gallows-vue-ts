<script setup lang="ts">
import { computed, defineComponent, ref, watch } from 'vue';
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
const wrongLetters = computed(() => letters.value.filter(letter =>
  !word.value.toLowerCase().includes(letter.toLowerCase())
))
const notification = ref<InstanceType<typeof GameNotification> | null>(null)
const popup = ref<InstanceType<typeof GamePopup> | null>(null)

watch(wrongLetters, () => {
  if (wrongLetters.value.length === 6) {
    popup.value?.open('lose')

  }
})
watch(correctLetters, () => {
  if (word.value.split("").every(x => correctLetters.value.includes(x.toLowerCase()))) {
    popup.value?.open('win')
  }

})
notification.value?.open()


window.addEventListener('keydown', ({ key }) => {
  if (letters.value.includes(key.toLocaleLowerCase())) {
    notification.value?.open()
    setTimeout(() => { notification.value?.close() }, 2000)
    return
  }
  if (/[а-яА-ЯёЁ]/.test(key)) {
    letters.value.push(key.toLowerCase())
  }
})
const restart = () => {
  letters.value = []
  popup.value?.close()
}
</script>
<template lang="">
  <GameHeader />
  <div class="game-container">
    <GameFigure :wrong-letters-count="wrongLetters.length"/>
    <GameWrongLetters :wrong-letters="wrongLetters"/>
    <GameWord :word="word" :correct-letters="correctLetters"/>
    <GamePopup ref="popup" @restart="restart" :word="word"/>
  </div>
  <GameNotification ref="notification"/>
</template>


<style lang=""></style>




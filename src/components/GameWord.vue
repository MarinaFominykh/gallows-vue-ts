<script setup lang="ts">
interface Props {
     word: string;
     correctLetters: string[];
}
defineProps<Props>();
</script>
<template lang="">
  <div class="word">
    <span v-for="(letter, index) in word" :key="index" class="letter">
      {{ correctLetters.includes(letter.toLowerCase()) ? letter : '' }}
    </span>
  </div>
</template>

<style lang=""></style>

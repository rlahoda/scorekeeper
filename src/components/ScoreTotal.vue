<script setup>
import { ref } from 'vue'
const props = defineProps(['scores'])
console.log('scores');
console.log(props.scores);
const scores = ref([...props.scores])
const scoreTotal = ref(0);

scores.value.forEach(score => {
  console.log('score value');
  console.log(score.value);
  if (score.value !== undefined) {
    console.log('has value');
    console.log(scoreTotal.value);
    console.log(score.value);
    scoreTotal.value = scoreTotal.value + score.value
  }
});

</script>

<template>
  <span class="score-total">{{ scoreTotal }}</span>
</template>

<style scoped>

</style>
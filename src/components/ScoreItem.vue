<script setup>
import { ref } from 'vue'
const props = defineProps(['score', 'showEdit', 'scoreIndex', 'playerIndex'])

const localScore = ref(props.score)

const emit = defineEmits(['scoreUpdate'])
function updateScore() {
    emit('scoreUpdate', {score: localScore, scoreIndex: props.scoreIndex, playerIndex: props.playerIndex})
  }

</script>

<template>
  <td>
    <input type="number" v-if="showEdit" v-model="localScore" @input="updateScore"/>  
    <span v-else>{{ score }}</span>
  </td>
</template>

<style scoped>

</style>
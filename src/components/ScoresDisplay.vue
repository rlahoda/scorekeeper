<script setup>
  import { ref } from 'vue'
  import ScoreItem from './ScoreItem.vue';
  import ScoreTotal from './ScoreTotal.vue';
  const props = defineProps(['players'])
  const emit = defineEmits(['playerUpdate'])
    
  const players = ref([...props.players])
  const showEdit = ref(false);
  
  function updatePlayers() {
    emit('playerUpdate', players.value)

  }

  function updateScore(data) {
    console.log('score updated');
    console.log({players});
    const {score, scoreIndex, playerIndex} = data;
    console.log({data});

    players.value[playerIndex].scores[scoreIndex] = score;
  }

  function handleEditClick() {
    showEdit.value = !showEdit.value
    if (showEdit.value === false) {
      updatePlayers()
    }
  }

  function addRound() {
    players.value.forEach(player => {
      player.scores.push(0)
    });
    updatePlayers();
  }


console.log(props.players);

</script>

<template>
  <div class="header">
    <button @click="handleEditClick">{{!showEdit ? 'Edit Scores' :  'Finish Editing'}}</button>
    <button @click="addRound">Add Round</button>
  </div>
  <table>
    <tr v-for="(player, i) in players" :key="i">
      <th>{{ player.name }}</th>
      <ScoreItem v-for="(score, index) in player.scores" :showEdit="index === player.scores.length - 1 ? true : showEdit" :score="score" :scoreIndex="index" :playerIndex="i" :players="players" :key="index" @scoreUpdate="updateScore">
      </ScoreItem>
      <ScoreTotal :scores="player.scores"></ScoreTotal>
    </tr>
  </table>
</template>

<style scoped>

</style>
<script setup>
  import { ref } from 'vue'
  const props = defineProps(['players'])
  const emit = defineEmits(['playerUpdate', 'finishedUpdate'])

  const playersArr = ref([...props.players])

  function updatePlayers() {
    emit('playerUpdate', playersArr.value)
  }
  function addPlayer() {
    playersArr.value.push({ name: '', scores: [0], id: Date()}) 
    updatePlayers();
  }

  function submitPlayers() {
    emit('finishedUpdate', playersArr.value)
  }
</script> 

<template>
  <div class="user-insert-background"></div>
  <div class="user-insert">
    <button v-if="playersArr.length < 1" @click=addPlayer>Click to add player</button>
    <form v-else @submit.prevent="submitPlayers">
      <ul>
        <li v-for="player in players" :key="player.id">
          Name: <input v-model="player.name" />
          Prior Score: <input v-model="player.scores[0]" />
        </li>
      </ul>
  <button type="button" @click=addPlayer>Add another player</button>
  <button>Submit</button>
</form>
</div>
</template>

<style scoped>
  .user-insert {
    position: absolute;
    top: 25%;
    left: 25%;
    background-color: orange;
    padding: 50px;
    border-radius: 10px;
  }

  .user-insert-background {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(134, 134, 134, 0.75);
    display: block;
    content: '';
  }
</style>
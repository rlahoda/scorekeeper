<script setup>
import { ref } from 'vue'
import UserAdd from './components/UserAdd.vue';
import ScoresDisplay from './components/ScoresDisplay.vue';

const players = ref([
  
  ])

const showUserInit = ref(true)

function handleInitialPlayerUpdate(data) {
  players.value = data;
  showUserInit.value = !showUserInit.value;
}


function handlePlayerUpdate(data) {
  players.value = data;
}

</script>

<template>
 
  <UserAdd v-if="showUserInit" :players="players" @playerUpdate="handlePlayerUpdate" @finishedUpdate="handleInitialPlayerUpdate">
  </UserAdd>
  <div v-else class="main">main
      <ScoresDisplay :players="players" @playerUpdate="handlePlayerUpdate"></ScoresDisplay>


    </div>

</template>

<style scoped>

</style>

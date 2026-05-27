<template>
  <header>
    <div class="header">
      <div class="text">ЗАПОМНИ СЛОВО</div>
      <Score :scoreNumber="score" />
    </div>
  </header>
  <div class="divider"></div>
  <div class="main-content">
    <Button v-if="!isStarted" @click="startGame">Начать игру</Button>
    <div v-if ="isStarted" class="cards-container">
      <Card v-for="(cardData, index) in cards" :key="cardData.key" :data="cardData" />
    </div>
  </div>
</template>

<script setup>
import Button from './components/Button.vue'
import Score from './components/Score.vue';
import Card from './components/Card.vue';
import { ref } from 'vue';

let score = ref("100");
let isStarted = ref(false);

const cards = ref([{
  key: 1,
  word: 'Aufschlag',
  translation: 'Подача',
  state: 'closed', // possible values: 'closed', 'open'
  status: 'pending' // possible values: 'pending', 'success', 'fail'
},
{
  key: 2,
  word: 'Bagger',
  translation: 'приём снизу',
  state: 'open',
  status: 'pending'
},
{
  key: 3,
  word: 'flach',
  translation: 'низкий',
  state: 'open',
  status: 'success'
},
{
  key: 4,
  word: 'vorne',
  translation: 'впереди',
  state: 'open',
  status: 'fail'
}]);

function startGame() {
  isStarted.value = true; 
}
</script>

<style scoped>
.text {
  font-family: 'Roboto', sans-serif;
  font-size: 16px;
  color: #222222;
  font-weight: bold;
}
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
}
.divider {
  height: 1px;
  margin: 20px 0;
}
.main-content {
  display: flex;
  justify-content: center;
  padding: 20px;
}
.cards-container {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: center;
  width: 100%;
}
</style>

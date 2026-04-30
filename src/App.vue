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
    <Card v-if="isStarted" :data="cardData" />
  </div>
</template>

<script setup>
import Button from './components/Button.vue'
import Score from './components/Score.vue';
import Card from './components/Card.vue';
import { ref } from 'vue';

let score = ref("100");
let isStarted = ref(false);

const cardData = ref({
  word: 'test word',
  translation: 'тестовое слово',
  state: 'closed', // possible values: 'closed', 'open'
  status: 'pending' // possible values: 'pending', 'success', 'fail'
});

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
</style>

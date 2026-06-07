<template>
  <div class="app-layout">
    <header>
      <div class="header">
        <div class="text">ЗАПОМНИ СЛОВО</div>
        <Score :scoreNumber="score" />
      </div>
    </header>
    <div class="divider"></div>
    <div class="main-content" :class="{ 'game-started': isStarted }">
      <div v-if ="isStarted" class="cards-container">
        <Card v-for="(cardData, index) in cards" :key="cardData.key" :data="cardData" @flip-card="flipCard(index)" @mark-success="markSuccess(index)" @mark-fail="markFail(index)" />
      </div>
      <Button class="game-btn" @click="startGame" :disabled="isLoading">
        {{ isStarted ? 'Начать заново' : 'Начать игру' }}
      </Button>
    </div>
  </div>
</template>

<script setup>
import Button from './components/Button.vue'
import Score from './components/Score.vue';
import Card from './components/Card.vue';
import { ref } from 'vue';

let score = ref(100);
let isStarted = ref(false);
const isLoading = ref(false);

const cards = ref([]);

async function fetchCards() {
  isLoading.value = true;
  try {
    const baseUrl = import.meta.env.VITE_API_BASE_URL;
    const response = await fetch(`${baseUrl}/api/random-words`);
    const data = await response.json();
    cards.value = data.map((item, index) => ({
      key: index + 1,
      word: item.word,
      translation: item.translation,
      state: 'closed',
      status: 'pending'
    }));
  }
  catch (error) {
    console.error('Error fetching cards:', error);
  }
  finally {
    isLoading.value = false;
  }
}

async function startGame() {
  await fetchCards();
  isStarted.value = true;
}

function flipCard(index) {
  cards.value[index].state = 
    cards.value[index].state === 'closed' ? 'open' : 'closed';
}

function markSuccess(index) {
  cards.value[index].status = 'success';
  score.value = score.value + 10;
}

function markFail(index) {
  cards.value[index].status = 'fail';
  score.value = score.value - 4;
}
</script>

<style scoped>
.app-layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  box-sizing: border-box;
  padding: 20px;
}
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
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.main-content.game-started {
  justify-content: flex-start;
  gap: 40px;
}
.game-btn {
  margin-top: 0;
}
.game-started .game-btn {
  margin-top: auto; /* Button stays at the bottom of the main content */
}
.cards-container {
  display: grid;
  grid-template-columns: repeat(5, 1fr); 
  gap: 40px 16px; 
  width: 100%;
  max-width: 1350px;
  margin: 0 auto;
}
</style>

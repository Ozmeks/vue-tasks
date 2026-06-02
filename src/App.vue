<template>
  <header>
    <div class="header">
      <div class="text">ЗАПОМНИ СЛОВО</div>
      <Score :scoreNumber="score" />
    </div>
  </header>
  <div class="divider"></div>
  <div class="main-content">
    <Button v-if="!isStarted" @click="startGame" :disabled="isLoading">Начать игру</Button>
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
  console.log('Fetched cards:', cards.value);
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

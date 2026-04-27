<template>
  <header>
    <div class="header">
      <div class="text">ЗАПОМНИ СЛОВО</div>
      <Score scoreNumber="100" />
    </div>
  </header>
  <div class="divider"></div>
  <div class="main-content">
    <Button>Начать игру</Button>
  </div>
</template>

<script setup>
import Button from './components/Button.vue'
import Score from './components/Score.vue';
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

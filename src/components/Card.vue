<template>
  <div class="card">
    <span class="badge badge-top card-text">01</span>
    <div class="card-content" @click="handleCardClick">
      <div class="card-text">{{ word }}</div>
    </div>
    <span class="badge badge-bottom card-text">ПЕРЕВЕРНУТЬ</span>
  </div>
</template>

<script setup>
const { word } = defineProps({
  word: {
    type: String,
    required: true
  }
});
const emit = defineEmits(["change-status", "flip-card"]);

function handleCardClick() {
  emit("change-status");
  emit("flip-card");
}

</script>

<style scoped>
.card {
  position: relative;
  width: 250px;
  height: 376px;
  border-radius: 16px;
}
.card-content {
  width: 100%;
  height: 100%;
  border-radius: 12px;
  border: 1px solid var(--color-bg-light);
  display: flex;
  align-items: center;
  justify-content: center;
}
.card-text {
  font-family: 'Roboto', sans-serif;
  font-size: 16px;
  font-weight: bold;
  color: #222222;
}
.card:hover {
  transform: scale(1.02);
  cursor: pointer;
}
.badge {
  position: absolute;
  background: white;
  padding: 2px 8px;
  font-size: 12px;
}
.badge-top {
  top: -10px;
  left: 10px;
}
.badge-bottom {
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
}
</style>
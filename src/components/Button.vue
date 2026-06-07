<template>
  <div class="button">
    <slot></slot>
  </div>
</template>

<script setup>
</script>

<style scoped>
.button {
  background-color: var(--color-bg-button);
  font-family: 'Roboto', sans-serif;
  font-size: 24px;
  align-items: center;
  justify-content: center;
  display: flex;
  color: var(--color-text-button);
  border-radius: 100px;
  width: 335px;
  height: 68px;
  cursor: pointer;
}
</style>
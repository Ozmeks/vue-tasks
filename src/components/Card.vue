<template>
  <div class="card">
    <svg style="display: none">
      <defs>
        <g id="fail-icon">
          <path fill-rule="evenodd" clip-rule="evenodd" d="M15.461 14.389L14.4 15.45L11.999 13.051L9.599 15.447L8.539 14.386L10.938 11.991L8.539 9.593L9.6 8.532L12 10.931L14.401 8.534L15.461 9.596L13.061 11.991L15.461 14.389ZM12 2.25C6.624 2.25 2.25 6.624 2.25 12C2.25 17.376 6.624 21.75 12 21.75C17.376 21.75 21.75 17.376 21.75 12C21.75 6.624 17.376 2.25 12 2.25Z" fill="#D00303"/>
        </g>
        <g id="success-icon">
          <path fill-rule="evenodd" clip-rule="evenodd" d="M12.4693 15.308L12.2543 15.689H11.4143L11.1613 15.353C11.1463 15.33 9.6593 13.108 7.7373 11.892L7.1023 11.492L7.9043 10.224L8.5373 10.624C9.92231 11.499 11.0723 12.777 11.7503 13.63C12.8153 12.025 15.3093 8.682 19.1343 5.971C17.3473 3.709 14.5863 2.25 11.4873 2.25C6.1113 2.25 1.7373 6.624 1.7373 12C1.7373 17.376 6.1113 21.75 11.4873 21.75C16.8633 21.75 21.2373 17.376 21.2373 12C21.2373 10.263 20.7753 8.635 19.9763 7.221C15.1433 10.667 12.4983 15.257 12.4693 15.308Z" fill="#09BB00"/>
        </g>
      </defs>
    </svg>

    <span class="badge badge-top card-text">{{ data.key }}</span>
    <div class="card-content" @click="emit('flip-card')">
      <div class="card-text">
        <div v-if="data.state === 'closed'">{{ data.word }}</div>
        <div v-else>{{ data.translation }}</div>
      </div>
    </div>
    <span v-if="data.state === 'closed'" class="badge badge-bottom card-text">ПЕРЕВЕРНУТЬ</span>
    <div v-else-if="data.status !== 'pending'">
      <div class="icon icon-top">
        <svg v-if="data.status === 'success'" width="36" height="36" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <use href="#success-icon"/>
        </svg>
        <svg v-else-if="data.status === 'fail'" width="36" height="36" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <use href="#fail-icon"/>
        </svg>
      </div>
      <span class="badge badge-bottom card-text">ЗАВЕРШЕНО</span>
    </div>
    <div v-else class="icon icon-bottom">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" @click="emit('mark-fail')">
        <use href="#fail-icon"/>
      </svg>
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" @click="emit('mark-success')">
        <use href="#success-icon"/>
      </svg>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const { data } = defineProps({
  data: {
    type: Object,
    required: true
  }
});
const emit = defineEmits(["flip-card", "mark-success", "mark-fail"]);

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
.icon {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  background: #FFFFFF;
}
.icon-bottom {
  bottom: -10px;
  gap: 10px;
}
.icon-top {
  top: -16px;
  left: 50%;
}
</style>
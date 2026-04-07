<script setup>
defineProps(['message'])
</script>

<template>
  <div class="error-container">
    <div class="error-icon">!</div>
    <h3 class="error-title">Oops! Something went wrong</h3>
    <p class="error-message">{{ message }}</p>
    <button @click="$emit('retry')" class="retry-btn">Try Again</button>
  </div>
</template>

<style scoped>
.error-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 5rem;
  background: rgba(255, 107, 107, 0.15);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  padding: 3rem;
  border-radius: 25px;
  border: 1px solid rgba(255, 107, 107, 0.3);
  max-width: 500px;
  margin-left: auto;
  margin-right: auto;
  box-shadow: 0 10px 40px rgba(255, 107, 107, 0.1);
}

.error-icon {
  width: 60px;
  height: 60px;
  background: #ff6b6b;
  border-radius: 50%;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  box-shadow: 0 0 20px rgba(255, 107, 107, 0.4);
}

.error-title {
  color: #fff;
  font-size: 1.5rem;
  margin-bottom: 0.8rem;
}

.error-message {
  color: rgba(255, 255, 255, 0.8);
  font-size: 1.1rem;
  margin-bottom: 2rem;
}

.retry-btn {
  background: white;
  color: #ff6b6b;
  border: none;
  padding: 12px 30px;
  border-radius: 30px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.retry-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
  background: #f8f8f8;
}

.retry-btn:active {
  transform: translateY(-1px);
}
</style>

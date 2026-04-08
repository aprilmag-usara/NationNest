<script setup>
const props = defineProps({
  modelValue: String,
  region: String
})
const emit = defineEmits(['update:modelValue', 'update:region'])

const regions = ['Africa', 'Americas', 'Asia', 'Europe', 'Oceania', 'Antarctic']

const updateValue = (event) => {
  emit('update:modelValue', event.target.value)}

const updateRegion = (event) => {
  emit('update:region', event.target.value)
}
</script>

<template>
  <div class="search-container">
    <div style="display: flex; gap: 10px; width: 100%; max-width: 700px;">
      <input 
        :value="modelValue"
        @input="updateValue"
        type="text" 
        class="search-box" 
        placeholder="🔍︎ Search for a nation, capital, or group..."
      />

      <select 
        :value="region"
        @change="updateRegion"
      >
        <option value="">All Continents</option>
        <option v-for="reg in regions" :key="reg" :value="reg">{{ reg }}</option>
      </select>
    </div>
  </div>
</template>

<style scoped>
.search-container {
  width: 100%;
  display: flex;
  justify-content: center;
  margin-bottom: 3rem;
}

.search-box {
  width: 100%;
  max-width: 600px;
  padding: 14px 28px;
  border-radius: 50px;
  border: 1px solid rgba(255, 255, 255, 0.3);
  font-size: 1.1rem;
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  color: white;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
  outline: none;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.search-box::placeholder {
  color: rgba(255, 255, 255, 0.7);
}

.search-box:focus {
  background: rgba(255, 255, 255, 0.25);
  transform: scale(1.02);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.3);
  border-color: rgba(255, 255, 255, 0.5);
}
</style>

<script setup>
import CountryCard from './CountryCard.vue'

const props = defineProps({
  countries: {
    type: Array,
    required: true
  }
})
</script>


<template>
  <div class="country-grid">
    <CountryCard 
      v-for="country in countries" 
      :key="country.cca3" 
      :country="country"
    />
  </div>
</template>

<style scoped>
.country-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 2.5rem;
  padding: 1.5rem 0;
  max-width: 1400px;
  margin: 0 auto;
}
</style>

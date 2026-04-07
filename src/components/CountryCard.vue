<script setup>
const props = defineProps({
  country: {
    type: Object,
    required: true
  }
})

const formatPopulation = (num) => {
  if (num === undefined || num === null) return 'N/A'
  return num.toLocaleString()
}
const handleImageError = (event) => {
  const countryCode = props.country.cca2 ? props.country.cca2.toLowerCase() : (props.country.cca3 ? props.country.cca3.substring(0, 2).toLowerCase() : 'af')
  event.target.src = `https://flagcdn.com/w320/${countryCode}.png`
}
</script>


<template>
  <div class="country-card">
    <img 
      :src="country.flags.png" 
      alt="flag" 
      class="flag-img"
      @error="handleImageError"
    />
    <div class="country-info">
      <h2>{{ country.name.common }}</h2>
      
      <div class="info-item">
        <span class="info-label">Capital:</span>
        <span class="info-value">{{ country.capital ? country.capital[0] : 'N/A' }}</span>
      </div>
      
      <div class="info-item">
        <span class="info-label">Region:</span>
        <span class="info-value">{{ country.region }}</span>
      </div>
      
      <div class="info-item">
        <span class="info-label">Population:</span>
        <span class="info-value">{{ formatPopulation(country.population) }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.country-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 20px;
  overflow: hidden;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  color: white;
  text-align: left;
  height: 100%;
  display: flex;
  flex-direction: column;
  box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.3);
}

.country-card:hover {
  transform: translateY(-15px) scale(1.02);
  box-shadow: 0 15px 35px rgba(0,0,0,0.5);
  background: rgba(255, 255, 255, 0.18);
  border-color: rgba(255, 255, 255, 0.4);
}

.flag-img {
  width: 100%;
  height: 180px;
  object-fit: cover;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.country-info {
  padding: 1.5rem;
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.country-info h2 {
  margin: 0 0 1.2rem 0;
  font-size: 1.5rem;
  font-weight: 700;
  color: #fff;
  text-shadow: 0 2px 4px rgba(0,0,0,0.3);
}

.info-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
}

.info-label {
  color: rgba(255, 255, 255, 0.7);
  font-weight: 500;
}

.info-value {
  color: white;
  font-weight: 600;
}
</style>

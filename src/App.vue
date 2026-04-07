<script setup>
import { ref, onMounted, computed } from 'vue'
import CountryList from './components/CountryList.vue'
import SearchCountry from './components/SearchCountry.vue'
import LoadingSpinner from './components/LoadingSpinner.vue'
import ErrorMessage from './components/ErrorMessage.vue'

const countries = ref([])
const searchQuery = ref('')
const loading = ref(true)
const error = ref(null)

const fetchCountries = async () => {
  try {
    loading.value = true
    error.value = null
    
    const response = await fetch('https://restcountries.com/v3.1/all?fields=name,capital,population,flags,region,cca3,cca2')
    if (!response.ok) {
      throw new Error('Failed to retrieve world data. Please check your connection.')
    }
    
    const data = await response.json()
    countries.value = data.sort((a, b) => a.name.common.localeCompare(b.name.common))
    
  } catch (err) {
    error.value = err.message
    console.error('Final error:', err)
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchCountries()
})

const filteredCountries = computed(() => {
  const query = (searchQuery.value || '').trim().toLowerCase()
  
  if (!query) return countries.value
  
  return countries.value.filter(country => {
    const name = (country.name?.common || '').toLowerCase()
    return name.startsWith(query)
  })
})
</script>


<template>
  <div class="app-wrapper">
    <div class="content-container">
      <header class="main-header">
        <h1 class="page-title">NationNest</h1>
        <p class="subtitle">Discover information about every nation across our community.</p>
      </header>

      <main>
        <SearchCountry v-model="searchQuery" />

        <LoadingSpinner v-if="loading" />

        <ErrorMessage 
          v-else-if="error" 
          :message="error" 
          @retry="fetchCountries" 
        />

        <div v-else>
          <CountryList 
            v-if="filteredCountries.length > 0" 
            :countries="filteredCountries" 
          />
          
          <div v-else class="empty-state">
            <p>No nations found matching "{{ searchQuery }}"</p>
          </div>
        </div>
      </main>

      <footer class="main-footer">
        <p>&copy; 2026 NationNest - Exploring the Community One Nation at a Time</p>
      </footer>
    </div>
  </div>
</template>

<style>
:root {
  --glass-bg: rgba(255, 255, 255, 0.1);
  --glass-border: rgba(255, 255, 255, 0.2);
  --glass-text: #ffffff;
}

body {
  margin: 0;
  padding: 0;
  font-family: 'Poppins', sans-serif;
  min-height: 100vh;
  background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), 
              url('https://images.unsplash.com/photo-1451187580459-43490279c0fa?q=80&w=2072&auto=format&fit=crop') no-repeat center center fixed;
  background-size: cover;
  color: white;
  -webkit-font-smoothing: antialiased;
}

.app-wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  padding: 2rem;
}

.content-container {
  max-width: 1400px;
  margin: 0 auto;
  width: 100%;
}

.main-header {
  text-align: center;
  margin-bottom: 3rem;
  padding-top: 2rem;
}

.page-title {
  font-size: 5rem;
  font-weight: 800;
  margin-bottom: 0.5rem;
  text-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  letter-spacing: -2px;
  background: linear-gradient(to right, #ffffff, #e0e0e0);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.subtitle {
  font-size: 1.4rem;
  color: rgba(255, 255, 255, 0.9);
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  font-weight: 300;
}

.empty-state {
  text-align: center;
  margin-top: 4rem;
  font-size: 1.5rem;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  padding: 3rem;
  border-radius: 25px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

.main-footer {
  margin-top: auto;
  text-align: center;
  padding: 4rem 0 2rem;
  color: rgba(255, 255, 255, 0.5);
  font-size: 0.9rem;
  letter-spacing: 1px;
}

@media (max-width: 768px) {
  .page-title {
    font-size: 3rem;
  }
  .subtitle {
    font-size: 1.1rem;
  }
  .app-wrapper {
    padding: 1rem;
  }
}
</style>

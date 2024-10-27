<script setup>
import { ref, onMounted } from 'vue'

const weatherData = ref(null)
const loading = ref(true)
const error = ref(null)

async function fetchWeatherData() {
  try {
    loading.value = true
    const response = await fetch('https://api.open-meteo.com/v1/forecast?latitude=45.5921&longitude=9.5734&hourly=temperature_2m')
    const data = await response.json()
    
    // Process the next 24 hours of data
    const currentHour = new Date().getHours()
    weatherData.value = data.hourly.time
      .slice(currentHour, currentHour + 24)
      .map((time, index) => ({
        time: new Date(time).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
        temperature: data.hourly.temperature_2m[currentHour + index]
      }))
  } catch (e) {
    error.value = 'Failed to load weather data'
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchWeatherData()
})
</script>

<template>
  <div class="weather">
    <h1>Milan Weather Forecast</h1>
    
    <div v-if="loading" class="loading">
      Loading weather data...
    </div>
    
    <div v-else-if="error" class="error">
      {{ error }}
    </div>
    
    <div v-else class="weather-card">
      <div class="weather-grid">
        <div v-for="(data, index) in weatherData" 
             :key="index" 
             class="weather-item">
          <div class="time">{{ data.time }}</div>
          <div class="temperature">{{ data.temperature }}°C</div>
        </div>
      </div>
      
      <button @click="fetchWeatherData" class="refresh-btn">
        Refresh Data
      </button>
    </div>
  </div>
</template>

<style scoped>
.weather {
  max-width: 1000px;
  margin: 0 auto;
}

.weather-card {
  background: #1a1a1a;
  border-radius: 8px;
  padding: 2rem;
  margin-top: 2rem;
}

.weather-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
  gap: 1rem;
  margin-bottom: 2rem;
}

.weather-item {
  background: #2c2c2c;
  padding: 1rem;
  border-radius: 6px;
  text-align: center;
}

.time {
  font-size: 0.9rem;
  color: #666;
  margin-bottom: 0.5rem;
}

.temperature {
  font-size: 1.2rem;
  font-weight: bold;
  color: #42b883;
}

.refresh-btn {
  width: 100%;
  max-width: 200px;
  margin: 0 auto;
  display: block;
}

.loading, .error {
  text-align: center;
  padding: 2rem;
  background: #1a1a1a;
  border-radius: 8px;
  margin-top: 2rem;
}

.error {
  color: #ff4444;
}

@media (prefers-color-scheme: light) {
  .weather-card {
    background: #f9f9f9;
  }

  .weather-item {
    background: #fff;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  }

  .loading, .error {
    background: #f9f9f9;
  }
}
</style>
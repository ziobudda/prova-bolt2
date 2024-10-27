<script setup>
import { ref } from 'vue'

const stats = ref([
  { label: 'Total Users', value: '1,234' },
  { label: 'Revenue', value: '$12,345' },
  { label: 'Active Projects', value: '42' }
])
</script>

<template>
  <div class="dashboard">
    <h1>Dashboard</h1>
    <div class="stats-grid">
      <div v-for="stat in stats" :key="stat.label" class="stat-card">
        <h3>{{ stat.label }}</h3>
        <p class="stat-value">{{ stat.value }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.dashboard {
  padding: 2rem;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin-top: 2rem;
}

.stat-card {
  background: #1a1a1a;
  padding: 1.5rem;
  border-radius: 8px;
  text-align: center;
}

.stat-value {
  font-size: 1.5rem;
  font-weight: bold;
  color: #646cff;
  margin-top: 0.5rem;
}

@media (prefers-color-scheme: light) {
  .stat-card {
    background: #f9f9f9;
  }
}
</style>
<script setup>
import AppSidebar from '../components/AppSidebar.vue'
</script>

<template>
  <div class="dashboard-layout">
    <AppSidebar />
    <main class="dashboard-content">
      <router-view />
    </main>
  </div>
</template>

<style scoped>
.dashboard-layout {
  display: flex;
  min-height: 100vh;
}

.dashboard-content {
  flex: 1;
  margin-left: 250px;
  padding: 2rem;
}
</style>
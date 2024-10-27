<script setup>
import { useAuthStore } from '../stores/auth'

const auth = useAuthStore()
</script>

<template>
  <div class="profile">
    <h1>Profile</h1>
    <div class="profile-card">
      <div class="profile-header">
        <div class="avatar">{{ auth.user?.email.charAt(0).toUpperCase() }}</div>
        <h2>{{ auth.user?.email }}</h2>
      </div>
      <div class="profile-info">
        <div class="info-item">
          <strong>Member Since:</strong>
          <span>January 1, 1970</span>
        </div>
        <div class="info-item">
          <strong>Role:</strong>
          <span>Administrator</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.profile {
  max-width: 800px;
  margin: 0 auto;
}

.profile-card {
  background: #1a1a1a;
  border-radius: 8px;
  padding: 2rem;
  margin-top: 2rem;
}

.profile-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.avatar {
  width: 60px;
  height: 60px;
  background: #42b883;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  font-weight: bold;
  color: white;
}

.profile-info {
  display: grid;
  gap: 1rem;
}

.info-item {
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 0;
  border-bottom: 1px solid #333;
}

.info-item:last-child {
  border-bottom: none;
}

@media (prefers-color-scheme: light) {
  .profile-card {
    background: #f9f9f9;
  }

  .info-item {
    border-bottom-color: #ddd;
  }
}
</style>
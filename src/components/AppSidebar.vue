<script setup>
import { useRouter } from 'vue-router'
import { useAuthStore } from '../stores/auth'

const router = useRouter()
const auth = useAuthStore()

const menuItems = [
  { icon: '📊', label: 'Dashboard', route: '/dashboard' },
  { icon: '🌤️', label: 'Weather', route: '/weather' },
  { icon: '👤', label: 'Profile', route: '/profile' },
  { icon: '⚙️', label: 'Settings', route: '/settings' }
]

function handleLogout() {
  auth.logout()
  router.push('/login')
}
</script>

<template>
  <aside class="sidebar">
    <div class="sidebar-header">
      <h3>Admin Panel</h3>
      <span class="user-email" v-if="auth.user">{{ auth.user.email }}</span>
    </div>
    
    <nav class="sidebar-nav">
      <router-link
        v-for="item in menuItems"
        :key="item.route"
        :to="item.route"
        class="nav-item"
        :class="{ active: $route.path === item.route }"
      >
        <span class="icon">{{ item.icon }}</span>
        {{ item.label }}
      </router-link>
    </nav>

    <div class="sidebar-footer">
      <button @click="handleLogout" class="logout-btn">
        <span class="icon">🚪</span> Logout
      </button>
    </div>
  </aside>
</template>

<style scoped>
.sidebar {
  width: 250px;
  height: 100vh;
  background: #1a1a1a;
  border-right: 1px solid #333;
  display: flex;
  flex-direction: column;
  position: fixed;
  left: 0;
  top: 0;
}

.sidebar-header {
  padding: 1.5rem;
  border-bottom: 1px solid #333;
}

.sidebar-header h3 {
  margin: 0;
  color: #42b883;
}

.user-email {
  font-size: 0.8rem;
  color: #666;
  display: block;
  margin-top: 0.5rem;
}

.sidebar-nav {
  flex: 1;
  padding: 1rem 0;
}

.nav-item {
  display: flex;
  align-items: center;
  padding: 0.75rem 1.5rem;
  color: #fff;
  text-decoration: none;
  transition: background-color 0.2s;
}

.nav-item:hover {
  background: #2c2c2c;
}

.nav-item.active {
  background: #2c2c2c;
  border-left: 3px solid #42b883;
}

.icon {
  margin-right: 0.75rem;
  font-size: 1.2rem;
}

.sidebar-footer {
  padding: 1rem 1.5rem;
  border-top: 1px solid #333;
}

.logout-btn {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: transparent;
  border: 1px solid #42b883;
  color: #42b883;
  padding: 0.5rem;
  cursor: pointer;
  transition: all 0.2s;
}

.logout-btn:hover {
  background: #42b883;
  color: #1a1a1a;
}

@media (prefers-color-scheme: light) {
  .sidebar {
    background: #f9f9f9;
    border-right-color: #ddd;
  }

  .nav-item {
    color: #213547;
  }

  .nav-item:hover {
    background: #eee;
  }

  .nav-item.active {
    background: #eee;
  }

  .sidebar-header,
  .sidebar-footer {
    border-color: #ddd;
  }
}
</style>
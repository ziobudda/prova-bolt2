<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { useAuthStore } from '../stores/auth'

const router = useRouter()
const auth = useAuthStore()

const credentials = ref({
  email: '',
  password: ''
})
const error = ref('')

async function handleLogin() {
  if (auth.login(credentials.value)) {
    router.push('/dashboard')
  } else {
    error.value = 'Invalid credentials. Try demo@example.com / demo'
  }
}
</script>

<template>
  <div class="login-container">
    <form @submit.prevent="handleLogin" class="login-form">
      <h1>Login</h1>
      
      <div class="form-group">
        <label for="email">Email</label>
        <input 
          id="email"
          type="email" 
          v-model="credentials.email"
          required
        >
      </div>

      <div class="form-group">
        <label for="password">Password</label>
        <input 
          id="password"
          type="password" 
          v-model="credentials.password"
          required
        >
      </div>

      <p v-if="error" class="error">{{ error }}</p>
      
      <button type="submit">Login</button>
    </form>
  </div>
</template>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 80vh;
}

.login-form {
  background: #1a1a1a;
  padding: 2rem;
  border-radius: 8px;
  width: 100%;
  max-width: 400px;
}

.form-group {
  margin-bottom: 1rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
}

input {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #333;
  border-radius: 4px;
  background: #2c2c2c;
  color: white;
}

button {
  width: 100%;
  margin-top: 1rem;
}

.error {
  color: #ff4444;
  margin-top: 1rem;
  font-size: 0.9rem;
}

@media (prefers-color-scheme: light) {
  .login-form {
    background: #f9f9f9;
  }

  input {
    background: white;
    border-color: #ddd;
    color: black;
  }
}
</style>
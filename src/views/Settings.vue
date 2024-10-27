<script setup>
import { ref } from 'vue'

const settings = ref({
  notifications: true,
  darkMode: true,
  language: 'en'
})

const languages = [
  { value: 'en', label: 'English' },
  { value: 'es', label: 'Spanish' },
  { value: 'fr', label: 'French' }
]
</script>

<template>
  <div class="settings">
    <h1>Settings</h1>
    <div class="settings-card">
      <div class="setting-item">
        <div class="setting-info">
          <h3>Notifications</h3>
          <p>Receive email notifications</p>
        </div>
        <label class="toggle">
          <input type="checkbox" v-model="settings.notifications">
          <span class="slider"></span>
        </label>
      </div>

      <div class="setting-item">
        <div class="setting-info">
          <h3>Dark Mode</h3>
          <p>Toggle dark/light theme</p>
        </div>
        <label class="toggle">
          <input type="checkbox" v-model="settings.darkMode">
          <span class="slider"></span>
        </label>
      </div>

      <div class="setting-item">
        <div class="setting-info">
          <h3>Language</h3>
          <p>Select your preferred language</p>
        </div>
        <select v-model="settings.language" class="language-select">
          <option v-for="lang in languages" :key="lang.value" :value="lang.value">
            {{ lang.label }}
          </option>
        </select>
      </div>
    </div>
  </div>
</template>

<style scoped>
.settings {
  max-width: 800px;
  margin: 0 auto;
}

.settings-card {
  background: #1a1a1a;
  border-radius: 8px;
  padding: 2rem;
  margin-top: 2rem;
}

.setting-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 0;
  border-bottom: 1px solid #333;
}

.setting-item:last-child {
  border-bottom: none;
}

.setting-info h3 {
  margin: 0;
  margin-bottom: 0.5rem;
}

.setting-info p {
  margin: 0;
  color: #666;
  font-size: 0.9rem;
}

.toggle {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.toggle input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #333;
  transition: .4s;
  border-radius: 34px;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  transition: .4s;
  border-radius: 50%;
}

input:checked + .slider {
  background-color: #42b883;
}

input:checked + .slider:before {
  transform: translateX(26px);
}

.language-select {
  padding: 0.5rem;
  border-radius: 4px;
  background: #2c2c2c;
  color: white;
  border: 1px solid #333;
}

@media (prefers-color-scheme: light) {
  .settings-card {
    background: #f9f9f9;
  }

  .setting-item {
    border-bottom-color: #ddd;
  }

  .language-select {
    background: white;
    border-color: #ddd;
    color: #213547;
  }

  .slider {
    background-color: #ddd;
  }

  .slider:before {
    background-color: #f9f9f9;
  }
}
</style>
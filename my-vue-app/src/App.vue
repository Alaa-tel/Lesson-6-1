<template>
  <div :class="['app', { dark: isDark }]">
    <div class="card">
      <button class="toggle" @click="toggleTheme">
        {{ isDark ? '☀️' : '🌙' }}
      </button>

      <img
        class="avatar"
        src="https://via.placeholder.com/120"
        alt="Profile"
      />

      <h1>Alaa</h1>
      <p class="tagline">Designer crafting thoughtful experiences</p>

      <div class="links">
        <a href="#" target="_blank">Portfolio</a>
        <a href="#" target="_blank">Dribbble</a>
        <a href="#" target="_blank">LinkedIn</a>
        <a href="mailto:you@email.com">Email</a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const isDark = ref(true)

onMounted(() => {
  const saved = localStorage.getItem('theme')
  if (saved) isDark.value = saved === 'dark'
})

function toggleTheme() {
  isDark.value = !isDark.value
  localStorage.setItem('theme', isDark.value ? 'dark' : 'light')
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
}

body {
  font-family: 'Inter', sans-serif;
}

/* Layout */
.app {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f5f5f5;
  transition: background 0.3s ease;
}

.app.dark {
  background: #0f0f0f;
}

/* Card */
.card {
  position: relative;
  width: 100%;
  max-width: 480px;
  padding: 32px 24px;
  border-radius: 16px;
  background: white;
  text-align: center;
  transition: all 0.3s ease;
}

.app.dark .card {
  background: #1a1a1a;
  color: white;
}

/* Avatar */
.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 16px;
}

/* Text */
h1 {
  font-size: 24px;
  margin-bottom: 8px;
}

.tagline {
  font-size: 14px;
  opacity: 0.7;
  margin-bottom: 24px;
}

/* Links */
.links {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.links a {
  text-decoration: none;
  padding: 12px;
  border-radius: 10px;
  background: #eeeeee;
  color: black;
  font-weight: 500;
  transition: all 0.2s ease;
}

.links a:hover {
  transform: translateY(-2px);
  background: #ddd;
}

.app.dark .links a {
  background: #2a2a2a;
  color: white;
}

.app.dark .links a:hover {
  background: #3a3a3a;
}

/* Toggle */
.toggle {
  position: absolute;
  top: 16px;
  right: 16px;
  border: none;
  background: transparent;
  font-size: 18px;
  cursor: pointer;
}
</style>

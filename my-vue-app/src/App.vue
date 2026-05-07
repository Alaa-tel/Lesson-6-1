<template>
  <v-app>
    <v-main>
      <v-container class="fill-height d-flex align-center">
        <v-row class="w-100" justify="center">
          <v-col cols="12" sm="8" md="6" lg="4">
            <v-card class="pa-8 text-center" elevation="2">
              <!-- Theme Toggle Button -->
              <div class="d-flex justify-end mb-4">
                <v-btn
                  icon
                  size="small"
                  variant="text"
                  @click="toggleTheme"
                >
                  <v-icon>{{ isDark ? 'mdi-white-balance-sunny' : 'mdi-moon-waning-crescent' }}</v-icon>
                </v-btn>
              </div>

              <!-- Profile Avatar -->
              <v-avatar
                size="120"
                class="mb-8"
                color="primary"
              >
                <span class="text-h3 font-weight-bold">A</span>
              </v-avatar>

              <!-- Name -->
              <h1 class="text-h4 mb-2 font-weight-600">Alaa</h1>

              <!-- Tagline -->
              <p class="text-body2 opacity-70 mb-8">
                Designer crafting thoughtful experiences
              </p>

              <!-- Link Buttons -->
              <div class="d-flex flex-column gap-5">
                <LinkButton
                  v-for="link in links"
                  :key="link.label"
                  :label="link.label"
                  :url="link.url"
                  :icon="link.icon"
                />
              </div>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'
import { useTheme } from 'vuetify'
import LinkButton from './components/LinkButton.vue'

const vuetifyTheme = useTheme()
const isDark = ref(true)

// Link buttons data
const links = [
  { label: 'Portfolio', url: '#', icon: 'mdi-briefcase' },
  { label: 'Dribbble', url: '#', icon: 'mdi-palette' },
  { label: 'LinkedIn', url: '#', icon: 'mdi-linkedin' },
  { label: 'Email', url: 'mailto:you@email.com', icon: 'mdi-email' }
]

// Initialize theme from localStorage or system preference
const initTheme = () => {
  const saved = localStorage.getItem('theme')
  if (saved) {
    isDark.value = saved === 'dark'
  } else {
    isDark.value = true
  }
  applyTheme()
}

// Apply theme to Vuetify
const applyTheme = () => {
  vuetifyTheme.global.name.value = isDark.value ? 'dark' : 'light'
}

// Toggle theme
const toggleTheme = () => {
  isDark.value = !isDark.value
  localStorage.setItem('theme', isDark.value ? 'dark' : 'light')
  applyTheme()
}

// Watch for theme changes
watch(isDark, () => {
  applyTheme()
})

// Initialize on mount
initTheme()
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap');

:root {
  font-family: 'Inter', sans-serif;
}

html, body {
  font-family: 'Inter', sans-serif;
}
</style>

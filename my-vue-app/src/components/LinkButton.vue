<template>
  <v-btn
    :href="url"
    target="_blank"
    variant="outlined"
    size="large"
    block
    class="text-none"
  >
    <v-icon start>{{ icon }}</v-icon>
    {{ label }}
  </v-btn>
</template>

<script setup lang="ts">
defineProps<{
  label: string
  url: string
  icon: string
}>()
</script>

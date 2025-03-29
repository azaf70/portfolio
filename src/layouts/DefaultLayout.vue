<script setup>
import { ParticlesBg } from '@/components/ui/particles-bg/index.js'
import { computed } from 'vue'
import { useColorMode } from '@vueuse/core'

const isDark = computed(() => useColorMode().value === 'dark')
</script>

<template>
  <div class="relative min-h-screen">
    <ParticlesBg
      class="fixed inset-0 z-10"
      :quantity="300"
      :ease="100"
      :color="isDark ? '#FFF' : '#000'"
      :staticity="10"
      refresh
    />
    <slot />
  </div>
</template>
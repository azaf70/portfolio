<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { useColorMode } from '@vueuse/core'
import { Menu, X } from 'lucide-vue-next'

const isMenuOpen = ref(false)
const isDark = useColorMode()
const scrollOpacity = ref(0)

const navLinks = [
  { name: 'About', path: '/about' },
  { name: 'Projects', path: '/projects' },
  { name: 'Contact', path: '/contact' },
]

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const handleScroll = () => {
  const scrollPosition = window.scrollY
  scrollOpacity.value = Math.min(scrollPosition / 200, 1)
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 backdrop-blur-2xl bg-white dark:bg-black border-b border-gray-200/20 dark:border-gray-800/30 rounded-b-2xl shadow-lg transition-all duration-300 ease-in-out"
    :style="{
      '--tw-backdrop-blur': `blur(${8 + scrollOpacity * 12}px)`,
      '--tw-bg-opacity': scrollOpacity * 0.9,
      backgroundColor: isDark.value
        ? `rgba(0, 0, 0, ${scrollOpacity * 0.9})`
        : `rgba(255, 255, 255, ${scrollOpacity * 0.9})`,
    }"
  >
    <nav class="container mx-auto px-4 py-4">
      <div class="flex items-center justify-between">
        <a
          href="/"
          class="text-2xl font-semibold bg-gradient-to-r from-white to-gray-300 bg-clip-text text-transparent dark:from-white dark:to-gray-400 transition-all duration-300 ease-in-out hover:scale-105"
        >
          AZAF
        </a>

        <!-- Desktop Navigation -->
        <div class="hidden md:flex items-center space-x-8">
          <template v-for="link in navLinks" :key="link.path">
            <a
              :href="link.path"
              class="text-gray-300 hover:text-white transition-all duration-300 ease-in-out text-sm font-medium rounded-lg px-3 py-2 hover:bg-white/10 dark:hover:bg-black/30 transform hover:scale-105"
            >
              {{ link.name }}
            </a>
          </template>
        </div>

        <!-- Mobile Menu Button -->
        <button
          @click="toggleMenu"
          class="md:hidden text-gray-300 hover:text-white focus:outline-none transition-transform duration-300 ease-in-out transform hover:scale-110"
        >
          <Menu v-if="!isMenuOpen" class="w-6 h-6" />
          <X v-else class="w-6 h-6" />
        </button>
      </div>

      <!-- Mobile Menu -->
      <transition
        enter-active-class="transition duration-300 ease-out"
        enter-from-class="transform -translate-y-full opacity-0"
        enter-to-class="transform translate-y-0 opacity-100"
        leave-active-class="transition duration-200 ease-in"
        leave-from-class="transform translate-y-0 opacity-100"
        leave-to-class="transform -translate-y-full opacity-0"
      >
        <div
          v-if="isMenuOpen"
          class="md:hidden mt-4 rounded-xl overflow-hidden bg-white/5 dark:bg-black/20 backdrop-blur-2xl"
        >
          <div class="flex flex-col space-y-2 p-4">
            <a
              v-for="link in navLinks"
              :key="link.path"
              :href="link.path"
              class="text-gray-300 hover:text-white transition-all duration-300 ease-in-out text-sm font-medium rounded-lg px-3 py-2 hover:bg-white/10 dark:hover:bg-black/30"
              @click="toggleMenu"
            >
              {{ link.name }}
            </a>
          </div>
        </div>
      </transition>
    </nav>
  </header>
</template>

<style scoped>
.backdrop-blur-md {
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
}
</style>

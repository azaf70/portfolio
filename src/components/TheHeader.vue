<script setup>
import { ref } from 'vue'
import { Menu, X } from 'lucide-vue-next'
import { NeonBorder } from '@/components/ui/neon-border/index.js'

const isMenuOpen = ref(false)

const navLinks = [
  { name: 'About', path: '/about' },
  { name: 'Projects', path: '/projects' },
  { name: 'Contact', path: '/contact' },
]

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}
</script>

<template>
  <NeonBorder animation-type="none" color1="#00cea8" color2="#bf61ff" duration="6">
    <header
      class="fixed top-0 left-0 right-0 z-50 backdrop-blur-2xl bg-white/5 dark:bg-black/10 border-b border-gray-200/20 dark:border-gray-800/30 rounded-b-2xl shadow-lg transition-all duration-300 ease-in-out hover:bg-white/15 dark:hover:bg-black/20"
    >
      <nav class="container mx-auto px-4 py-4">
        <div class="flex items-center justify-between">
          <img src="/logo.png" alt="Logo" class="h-14 object-contain" />

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
            class="md:hidden text-gray-300 hover:text-white focus:outline-none transition-transform duration-300 ease-in-out transform hover:scale-110"
            @click="toggleMenu"
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
  </NeonBorder>
</template>

<style scoped>
.backdrop-blur-md {
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
}
</style>

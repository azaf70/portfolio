<script setup>
import { computed } from 'vue'
import { useColorMode } from '@vueuse/core'
import { ParticlesBg } from '@/components/ui/particles-bg/index.js'
import { ShimmerButton } from '@/components/ui/shimmer-button/index.js'

const isDark = computed(() => useColorMode().value === 'dark')
</script>

<template>
  <div
    class="relative flex w-full min-h-screen flex-col items-center justify-center overflow-hidden rounded-lg border bg-background md:shadow-xl"
  >
    <Transition
      appear
      enter-active-class="transition duration-400 ease-out"
      enter-from-class="opacity-0 translate-y-5"
      enter-to-class="opacity-100 translate-y-0"
    >
      <div class="text-center px-6">
        <h1 class="text-white mb-4 text-4xl font-bold sm:text-5xl md:text-6xl">
          Hi, I'm
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-[#00cea8] to-[#bf61ff]"
            >Abdullah Zafar</span
          >
        </h1>
        <p class="text-white/80 max-w-3xl mx-auto text-lg sm:text-xl md:text-2xl">
          I develop web applications, user interfaces and create digital experiences that leave a
          lasting impression.
        </p>

        <Transition
          appear
          enter-active-class="transition duration-400 delay-200 ease-out"
          enter-from-class="opacity-0 translate-y-5"
          enter-to-class="opacity-100 translate-y-0"
        >
          <div class="mt-8 flex gap-2 justify-center">
            <ShimmerButton class="shadow-2xl" shimmer-size="2px">
              <span
                class="whitespace-pre-wrap text-center text-sm font-medium leading-none tracking-tight text-white lg:text-lg dark:from-white dark:to-slate-900/10"
              >
                View My Work
              </span>
            </ShimmerButton>
          </div>
        </Transition>
      </div>
    </Transition>
    <ParticlesBg
      class="absolute inset-0"
      :quantity="300"
      :ease="100"
      :color="isDark ? '#FFF' : '#000'"
      :staticity="10"
      refresh
    />
  </div>
</template>
<style scoped></style>

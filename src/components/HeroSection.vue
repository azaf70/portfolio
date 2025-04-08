<script setup>
import { ShimmerButton } from '@/components/ui/shimmer-button/index.js'
import { FlipWords } from '@/components/ui/flip-words/index.js'
import { BlurReveal } from '@/components/ui/blur-reveal/index.js'
</script>

<template>
  <div
    class="relative flex w-full min-h-screen flex-col items-center justify-center overflow-hidden rounded-lg border-t bg-background md:shadow-xl"
  >
    <Transition
      appear
      enter-active-class="transition duration-400 ease-out"
      enter-from-class="opacity-0 translate-y-5"
      enter-to-class="opacity-100 translate-y-0"
    >
      <div class="text-center px-6">
        <BlurReveal :delay="0.2" :duration="0.75" class="p-8">
          <h1
            class="text-white mb-4 text-4xl font-bold sm:text-5xl md:text-6xl transition duration-700 ease-in-out"
          >
            Hi, I'm
            <FlipWords
              :duration="3000"
              :words="['Abdullah Zafar', 'A Full Stack Developer', 'Performant', 'Versatile']"
              class="inline-block bg-clip-text bg-gradient-to-r from-teal-400 via-purple-500 to-indigo-500 bg-[length:200%_auto] animate-gradient-x font-bold transition-all duration-500 ease-in-out [text-shadow:_0_0_80px_rgb(45_212_191_/_70%),_0_0_40px_rgb(147_51_234_/_60%),_0_0_20px_rgb(99_102_241_/_50%)]"
            />
          </h1>
          <p class="text-white/80 max-w-4xl mx-auto text-lg sm:text-xl md:text-2xl">
            I develop web applications, user interfaces and create digital experiences that leave a
            lasting impression.
          </p>
        </BlurReveal>

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
  </div>
</template>

<style scoped></style>

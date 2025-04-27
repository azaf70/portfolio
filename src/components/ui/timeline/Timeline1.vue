<template>
  <div
    ref="timelineContainerRef"
    class="w-full font-sans px-4 mx-4 sm:px-6 md:px-8 lg:px-10 dark:bg-neutral-950"
  >
    <!-- Header -->
    <div class="mx-auto max-w-7xl py-12 sm:py-16 md:py-20 text-center">
      <h2 class="text-xl sm:text-2xl md:text-4xl font-bold text-neutral-900 dark:text-white">
        {{ title }}
      </h2>
      <p class="mt-2 text-sm sm:text-base md:text-lg text-neutral-700 dark:text-neutral-300">
        {{ description }}
      </p>
    </div>

    <!-- Timeline -->
    <div ref="timelineRef" class="relative mx-auto max-w-7xl pb-20 timeline">
      <!-- Static line background (desktop only) -->
      <div
        class="hidden md:block absolute left-1/2 top-0 w-[2px] h-full bg-neutral-200 dark:bg-neutral-700"
      ></div>

      <!-- Animated beam -->
      <Motion
        as="div"
        class="hidden md:block absolute left-1/2 top-0 w-[2px] rounded-full bg-gradient-to-t from-[#bf61ff] via-[#00cea8] to-transparent"
        :style="{
          height: lineHeight,
          opacity: lineOpacity,
        }"
      />

      <!-- Timeline entries -->
      <div
        v-for="(item, i) in items"
        :key="item.id"
        class="flex flex-col md:flex-row items-start md:items-center gap-6 py-8"
      >
        <!-- Bullet + Label -->
        <Motion
          as="div"
          class="relative flex items-center md:w-1/3"
          :initial="{ opacity: 0, x: -50 }"
          :in-view="{ opacity: 1, x: 0 }"
          :transition="{ type: 'spring', stiffness: 80, damping: 12, delay: i * 0.1 }"
          viewport="{ amount: 0.2, once: false }"
        >
          <div
            class="absolute -left-6 sm:-left-8 w-4 h-4 sm:w-6 sm:h-6 rounded-full bg-white dark:bg-black border border-neutral-300 dark:border-neutral-600"
          />
          <h3
            class="pl-8 text-lg sm:text-xl md:text-2xl font-bold text-neutral-800 dark:text-neutral-200"
          >
            {{ item.label }}
          </h3>
        </Motion>

        <!-- Content -->
        <Motion
          as="div"
          class="md:flex-1"
          :initial="{ opacity: 0, y: 50 }"
          :in-view="{ opacity: 1, y: 0 }"
          :transition="{ type: 'spring', stiffness: 80, damping: 12, delay: i * 0.1 + 0.05 }"
          viewport="{ amount: 0.2, once: false }"
        >
          <slot :name="item.id" />
        </Motion>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Motion, useScroll, useTransform } from 'motion-v'

const props = defineProps({
  items: { type: Array, default: () => [] },
  title: { type: String, default: '' },
  description: { type: String, default: '' },
})

const timelineContainerRef = ref(null)
const timelineRef = ref(null)
const containerHeight = ref(0)

// Measure how tall the timeline is
onMounted(() => {
  if (timelineRef.value) {
    containerHeight.value = timelineRef.value.getBoundingClientRect().height
  }
})

// Track scroll progress through the container
const { scrollYProgress } = useScroll({
  target: timelineContainerRef,
  offset: ['start start', 'end end'],
})

// Beam grows from 0 → full height
const lineHeight = useTransform(scrollYProgress, [0, 1], [0, containerHeight.value])
// Beam fades in at the top, then stays opaque
const lineOpacity = useTransform(scrollYProgress, [0, 0.05, 0.1], [0, 1, 1])
</script>

<style scoped>
.timeline {
  position: relative;
}
</style>

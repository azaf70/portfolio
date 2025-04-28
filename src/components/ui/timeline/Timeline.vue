<template>
  <div ref="timelineContainerRef" class="w-full text-white px-4 sm:px-6 lg:px-8 py-16">
    <div class="relative mx-auto max-w-5xl">
      <!-- Static center line (desktop only) -->
      <div class="hidden md:block absolute inset-y-0 left-1/2 w-px bg-neutral-700" />

      <!-- Animated beam (desktop only) -->
      <Motion
        as="div"
        class="hidden md:block absolute inset-y-0 left-1/2 w-px rounded-full bg-gradient-to-t from-[#bf61ff] via-[#00cea8] to-transparent"
        :style="{ height: beamHeight, opacity: beamOpacity }"
      />

      <!-- Timeline entries -->
      <div
        v-for="(item, i) in items"
        :key="item.id"
        class="grid grid-cols-1 md:grid-cols-[1fr_auto_1fr] gap-y-32 lg:gap-y-48 xl:gap-y-64 items-start"
      >
        <!-- LEFT PANEL (even items) -->
        <Motion
          v-if="i % 2 === 0"
          as="div"
          class="col-start-1 col-end-2 md:col-start-1 md:col-end-2 bg-neutral-800/50 rounded-2xl p-4 md:p-8 shadow-lg my-12"
          :initial="{ opacity: 0, x: -60 }"
          :in-view="{ opacity: 1, x: 0 }"
          :transition="{ type: 'spring', stiffness: 90, damping: 14, delay: i * 0.15 }"
          viewport="{ amount: 0.3, once: false }"
        >
          <h3 class="text-2xl lg:text-3xl font-extrabold mb-3">{{ item.title }}</h3>
          <p class="font-semibold text-lg lg:text-xl mb-1 text-neutral-300">
            {{ item.company_name }}
          </p>
          <p class="text-sm lg:text-base mb-4 text-neutral-500">{{ item.date }}</p>
          <ul class="list-disc list-inside space-y-2 text-neutral-300">
            <li v-for="(p, idx) in item.points" :key="idx">{{ p }}</li>
          </ul>
        </Motion>

        <!-- spacer on mobile / when odd -->
        <div v-else class="col-start-1 col-end-2 md:hidden h-16" />

        <!-- CENTER BULLET (desktop only) -->
        <!-- CENTER BULLET (desktop only) -->
        <div class="hidden md:block col-start-2 col-end-3 relative">
          <div class="absolute top-8 left-1/2 transform -translate-x-1/2">
            <!-- outer: gradient background + padding -->
            <div class="p-1 bg-gradient-to-br from-[#bf61ff] to-[#00cea8] rounded-full">
              <!-- inner: transparent circle -->
              <div class="w-3 h-3 lg:w-4 lg:h-4 bg-white/40 rounded-full"></div>
            </div>
          </div>
        </div>

        <!-- RIGHT PANEL (odd items) -->
        <Motion
          v-if="i % 2 === 1"
          as="div"
          class="col-start-1 col-end-2 md:col-start-3 md:col-end-4 bg-neutral-800/50 rounded-2xl p-4 md:p-8 shadow-lg my-12"
          :initial="{ opacity: 0, x: 60 }"
          :in-view="{ opacity: 1, x: 0 }"
          :transition="{ type: 'spring', stiffness: 90, damping: 14, delay: i * 0.15 }"
          viewport="{ amount: 0.3, once: false }"
        >
          <h3 class="text-2xl lg:text-3xl font-extrabold mb-3">{{ item.title }}</h3>
          <p class="font-semibold text-lg lg:text-xl mb-1 text-neutral-300">
            {{ item.company_name }}
          </p>
          <p class="text-sm lg:text-base mb-4 text-neutral-500">{{ item.date }}</p>
          <ul class="list-disc list-inside space-y-2 text-neutral-300">
            <li v-for="(p, idx) in item.points" :key="idx">{{ p }}</li>
          </ul>
        </Motion>

        <!-- spacer on mobile / when even -->
        <div v-else class="col-start-1 col-end-2 md:hidden h-16" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { Motion, useScroll, useTransform } from 'motion-v'

interface Item {
  id: string
  title: string
  company_name: string
  date: string
  points: string[]
}

const props = withDefaults(defineProps<{ items?: Item[] }>(), { items: () => [] })

const timelineContainerRef = ref<HTMLElement | null>(null)
const containerHeight = ref(0)

onMounted(() => {
  if (timelineContainerRef.value) {
    containerHeight.value = timelineContainerRef.value.getBoundingClientRect().height
  }
})

const { scrollYProgress } = useScroll({
  target: timelineContainerRef,
  offset: ['start start', 'end end'],
})

const beamHeight = useTransform(scrollYProgress, [0, 1], [0, containerHeight.value])
const beamOpacity = useTransform(scrollYProgress, [0, 0.1], [0, 1])
</script>

<style scoped>
/* Everything is handled in Tailwind classes */
</style>

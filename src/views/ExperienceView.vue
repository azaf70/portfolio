<script setup>
import SectionHeader from '@/components/SectionHeader.vue'
import { ScrollReveal } from '@/components/ui/scroll-reveal/index.js'
import { Timeline } from '@/components/ui/timeline/index.js'

const data = [
  {
    id: 'version1.0',
    label: 'Version 1.0',
  },
  {
    id: 'version2.0',
    label: 'Version 2.0',
  },

  {
    id: 'version3.0',
    label: 'Version 3.0',
  },
  {
    id: 'version4.0',
    label: 'Version 4.0',
  },

  {
    id: 'version5.0',
    label: 'Version 5.0',
  },
  {
    id: 'version6.0',
    label: 'Version 6.0',
  },
]
</script>

<template>
  <ScrollReveal direction="down" :delay="200">
    <SectionHeader subtitle="About my experience" title="Experience" />
    <div class="h-fit w-full">
      <Timeline
        :items="data"
        title="My Journey"
        description="A timeline of my professional experience and achievements"
      >
        <template v-for="(item, index) in data" :key="item.id + 'template'" #[item.id]>
          <div class="relative w-full pr-4 pl-16 md:pl-4 lg:pl-8">
            <h3
              class="mb-2 sm:mb-4 block text-left text-xl sm:text-2xl md:text-3xl font-bold text-white/90 dark:text-white"
            >
              {{ `Section ${index + 1}` }}
            </h3>
            <p
              class="mb-4 sm:mb-6 md:mb-8 text-sm sm:text-base md:text-lg font-normal text-white/70 dark:text-white/70 max-w-xl"
            >
              Inspira UI gives you the freedom to design awesome website, in less time.
            </p>
          </div>
        </template>
      </Timeline>
    </div>
  </ScrollReveal>
</template>

<style scoped></style>

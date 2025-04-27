<script setup>
import SectionHeader from '@/components/SectionHeader.vue'
import { GlareCard } from '@/components/ui/glare-card/index.js'
import { ScrollReveal } from '@/components/ui/scroll-reveal/index.js'
import { NumberTicker } from '@/components/ui/number-ticker/index.js'
</script>

<template>
  <ScrollReveal direction="down" :delay="200" class="min-h-full">
    <SectionHeader subtitle="Software Developer" title="About Me" />
    <main
      id="content"
      class="max-w-6xl px-4 sm:px-6 lg:px-8 flex flex-col justify-center sm:items-center mx-auto py-8"
    >
      <ScrollReveal direction="up" :delay="400">
        <div class="text-center py-8 px-4 sm:px-6 lg:px-8">
          <p class="text-white/80 mx-auto text-md sm:text-xl">
            Experienced professional with a successful track record of
            <span
              class="bg-clip-text bg-gradient-to-r from-teal-400 via-purple-500 to-indigo-500 bg-[length:200%_auto] animate-gradient-x font-bold transition-all duration-500 ease-in-out"
            >
              <NumberTicker decimal-places="1" :value="4" />
            </span>
            years in maintaining, enhancing, and developing both legacy systems and public-facing
            applications on a commercial level. Proficient in utilizing the latest technologies to
            create dynamic web applications that drive optimal user experiences. Known for
            delivering exceptional user support and maximizing efficiency in Agile environments.
          </p>
        </div>
      </ScrollReveal>
      <div class="grid lg:grid-cols-4 md:grid-cols-2 grid-cols-1 gap-6 w-full">
        <ScrollReveal direction="up" :delay="600">
          <GlareCard class="flex flex-col items-center justify-center p-6 min-h-[200px] w-full">
            <h3 class="text-xl font-bold mb-3 text-white">Frontend</h3>
            <p class="text-white/80 text-center">
              Vue.js, React, TypeScript, Tailwind CSS, Modern UI/UX
            </p>
          </GlareCard>
        </ScrollReveal>
        <ScrollReveal direction="up" :delay="800">
          <GlareCard class="flex flex-col items-center justify-center p-6 min-h-[200px] w-full">
            <h3 class="text-xl font-bold mb-3 text-white">Backend</h3>
            <p class="text-white/80 text-center">
              Laravel, Node.js, RESTful APIs, Database Management
            </p>
          </GlareCard>
        </ScrollReveal>
        <ScrollReveal direction="up" :delay="1000">
          <GlareCard class="flex flex-col items-center justify-center p-6 min-h-[200px] w-full">
            <h3 class="text-xl font-bold mb-3 text-white">DevOps</h3>
            <p class="text-white/80 text-center">
              CI/CD, Docker, Cloud Services, Performance Optimization
            </p>
          </GlareCard>
        </ScrollReveal>
        <ScrollReveal direction="up" :delay="1200">
          <GlareCard class="flex flex-col items-center justify-center p-6 min-h-[200px] w-full">
            <h3 class="text-xl font-bold mb-3 text-white">Soft Skills</h3>
            <p class="text-white/80 text-center">
              Agile Methodology, Team Leadership, Problem Solving
            </p>
          </GlareCard>
        </ScrollReveal>
      </div>
    </main>
  </ScrollReveal>
</template>

<style scoped></style>

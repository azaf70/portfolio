<script setup>
import SectionHeader from '@/components/SectionHeader.vue'
import { GlareCard } from '@/components/ui/glare-card/index.js'
</script>

<template>
  <SectionHeader subtitle="Software Developer" title="About Me" />
  <main
    id="content"
    class="max-w-6xl px-4 sm:px-6 lg:px-8 flex flex-col justify-center sm:items-center mx-auto py-8"
  >
    <div class="text-center py-8 px-4 sm:px-6 lg:px-8">
      <p class="text-white/80 mx-auto text-md sm:text-xl">
        Experienced professional with a successful track record of 4+ years in maintaining,
        enhancing, and developing both legacy systems and public-facing applications on a commercial
        level. Proficient in utilizing the latest technologies to create dynamic web applications
        that drive optimal user experiences. Known for delivering exceptional user support and
        maximizing efficiency in Agile environments.
      </p>
    </div>
    <div class="grid lg:grid-cols-4 md:grid-cols-2 grid-cols-1 gap-6 w-full">
      <GlareCard class="flex flex-col items-center justify-center p-6 min-h-[200px] w-full">
        <h3 class="text-xl font-bold mb-3 text-white">Frontend</h3>
        <p class="text-white/80 text-center">
          Vue.js, React, TypeScript, Tailwind CSS, Modern UI/UX
        </p>
      </GlareCard>
      <GlareCard class="flex flex-col items-center justify-center p-6 min-h-[200px] w-full">
        <h3 class="text-xl font-bold mb-3 text-white">Backend</h3>
        <p class="text-white/80 text-center">Laravel, Node.js, RESTful APIs, Database Management</p>
      </GlareCard>
      <GlareCard class="flex flex-col items-center justify-center p-6 min-h-[200px] w-full">
        <h3 class="text-xl font-bold mb-3 text-white">DevOps</h3>
        <p class="text-white/80 text-center">
          CI/CD, Docker, Cloud Services, Performance Optimization
        </p>
      </GlareCard>
      <GlareCard class="flex flex-col items-center justify-center p-6 min-h-[200px] w-full">
        <h3 class="text-xl font-bold mb-3 text-white">Soft Skills</h3>
        <p class="text-white/80 text-center">Agile Methodology, Team Leadership, Problem Solving</p>
      </GlareCard>
    </div>
  </main>
</template>

<style scoped></style>

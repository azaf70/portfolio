<script setup>
import SectionHeader from '@/components/SectionHeader.vue'
import { ScrollReveal } from '@/components/ui/scroll-reveal/index.js'
import { Timeline } from '@/components/ui/timeline/index.js'

const experiences = [
  {
    id: 'crown-gas',
    label: '2021 - Present',
    title: 'Software Engineer',
    company_name: 'Crown Gas & Power',
    iconBg: '#E6DEDD',
    date: 'May 2021 - Present',
    points: [
      'Developed public-facing applications enhancing customer engagement.',
      'Automated internal workflows saving over 30 hours per week.',
      'Optimized performance and responsiveness of web platforms.',
      'Integrated secure and scalable backend features with front-end systems.',
      'Collaborated closely with UX/UI teams and backend engineers.',
    ],
  },
  {
    id: 'deeper-digital',
    label: '2021',
    title: 'Digital Engineer',
    company_name: 'Deeper Digital Engineer Programme',
    iconBg: '#383E56',
    date: 'Jan 2021 - May 2021',
    points: [
      'Gained strong foundations in PHP, MySQL, JS, HTML & CSS.',
      'Built projects simulating real-world dev challenges.',
      'Enhanced understanding of full stack development workflows.',
    ],
  },
  {
    id: 'it-career',
    label: '2020 - 2021',
    title: 'Full Stack Engineer Trainee',
    company_name: 'IT Career Switch',
    iconBg: '#E6DEDD',
    date: 'Nov 2020 - May 2021',
    points: [
      'Completed a structured program with full-stack focus.',
      'Worked on practical projects and obtained certifications.',
      'Gained real-world readiness with a robust portfolio.',
    ],
  },
  {
    id: 'ebay',
    label: '2015 - 2022',
    title: 'Entrepreneur',
    company_name: 'eBay',
    iconBg: '#383E56',
    date: 'Aug 2015 - Aug 2022',
    points: [
      'Improved communication and customer interaction through sales.',
      'Gained time management and problem-solving experience.',
      'Used software skills to manage and automate listings.',
    ],
  },
]
</script>

<template>
  <ScrollReveal direction="down" :delay="200">
    <SectionHeader subtitle="About my experience" title="Experience" />
    <div class="h-fit w-full">
      <Timeline
        :items="experiences"
        title="My Journey"
        description="A timeline of my professional experience and achievements"
      />
    </div>
  </ScrollReveal>
</template>

<style scoped></style>

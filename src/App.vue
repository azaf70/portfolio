<script setup>
import TheHeader from '@/components/TheHeader.vue'
import HeroSection from '@/components/HeroSection.vue'
import IntroductionView from '@/views/IntroductionView.vue'
import DefaultLayout from '@/layouts/DefaultLayout.vue'
import ExperienceView from '@/views/ExperienceView.vue'
</script>

<template>
  <DefaultLayout>
    <TheHeader />
    <HeroSection />
    <IntroductionView />
    <ExperienceView />
    <IntroductionView />
  </DefaultLayout>
</template>

<style scoped></style>

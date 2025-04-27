<script setup>
import { ref } from 'vue'
import { useMotion } from '@vueuse/motion'
import { useIntersectionObserver } from '@vueuse/core'

const props = defineProps({
  direction: {
    type: String,
    default: 'up',
    validator: (v) => ['up', 'down', 'left', 'right'].includes(v),
  },
  distance: { type: Number, default: 50 },
  duration: { type: Number, default: 800 },
  delay: { type: Number, default: 0 },
  threshold: { type: Number, default: 0.1 },
})

const el = ref(null)

const initial = {
  opacity: 0,
  x:
    props.direction === 'left' ? props.distance : props.direction === 'right' ? -props.distance : 0,
  y: props.direction === 'up' ? props.distance : props.direction === 'down' ? -props.distance : 0,
}

const enter = {
  opacity: 1,
  x: 0,
  y: 0,
  transition: {
    type: 'spring',
    stiffness: 100,
    damping: 20,
    duration: props.duration,
    delay: props.delay,
  },
}

// Initialize the motion controller once:
const motion = useMotion(el, { initial, enter })

// Observe continuously, toggling on entry/exit:
useIntersectionObserver(
  el,
  ([{ isIntersecting }]) => {
    if (isIntersecting) {
      motion.apply('enter')
    } else {
      motion.apply('initial')
    }
  },
  { threshold: props.threshold }
)
</script>

<template>
  <div ref="el" class="scroll-reveal">
    <slot />
  </div>
</template>

<style scoped>
.scroll-reveal {
  will-change: transform, opacity;
}
</style>

<template>
  <span
    ref="spanRef"
    class="text-transparent bg-clip-text bg-gradient-to-r from-teal-400 via-purple-500 to-indigo-500 bg-[length:200%_auto] animate-gradient-x font-bold transition-all duration-500 ease-in-out"
    :class="cn('inline-block tabular-nums tracking-wider', props.class)"
  >
    {{ output }}+
  </span>
</template>

<script setup>
import { TransitionPresets, useElementVisibility, useTransition } from '@vueuse/core'
import { cn } from '@/lib/utils'
import { ref, watch, computed } from 'vue'

const props = defineProps({
  value: { type: Number, required: true, default: 0 },
  direction: { type: String, required: false, default: 'up' },
  duration: { type: Number, required: false, default: 1000 },
  delay: { type: Number, required: false, default: 0 },
  decimalPlaces: { type: Number, required: false, default: 2 },
  class: { type: String, required: false },
  transition: { type: null, required: false, default: 'easeOutCubic' },
})

const spanRef = ref()

const transitionValue = ref(props.direction === 'down' ? props.value : 0)

const transitionOutput = useTransition(transitionValue, {
  delay: props.delay,
  duration: props.duration,
  transition: TransitionPresets[props.transition],
})

const output = computed(() => {
  return new Intl.NumberFormat('en-US', {
    minimumFractionDigits: props.decimalPlaces,
    maximumFractionDigits: props.decimalPlaces,
  }).format(Number(transitionOutput.value.toFixed(props.decimalPlaces)))
})

const isInView = useElementVisibility(spanRef, {
  threshold: 0,
})

const hasBeenInView = ref(false)

const stopIsInViewWatcher = watch(
  isInView,
  (isVisible) => {
    if (isVisible && !hasBeenInView.value) {
      hasBeenInView.value = true
      transitionValue.value = props.direction === 'down' ? 0 : props.value
      stopIsInViewWatcher()
    }
  },
  { immediate: true }
)

watch(
  () => props.value,
  (newVal) => {
    if (hasBeenInView.value) {
      transitionValue.value = props.direction === 'down' ? 0 : newVal
    }
  }
)
</script>

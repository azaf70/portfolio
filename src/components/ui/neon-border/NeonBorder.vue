<template>
  <div :class="cn(
  'relative inline-block h-10 w-full overflow-hidden rounded-lg p-px z-10',
  props.class,
)">
    <div :class="cn(
  'neon-border-one rounded-lg',
  animationType !== 'none' ? 'animate-border' : '',
)"></div>
    <div :class="cn(
  'neon-border-two rounded-lg',
  animationType !== 'none' ? 'animate-border' : '',
)"></div>
    <slot> </slot>
  </div>
</template>

<script setup>
import { cn } from '@/lib/utils';
import { computed } from 'vue';

const props = defineProps({
  color1: { type: String, required: false, default: '#0496ff' },
  color2: { type: String, required: false, default: '#ff0a54' },
  animationType: { type: String, required: false, default: 'half' },
  duration: { type: Number, required: false, default: 6 },
  class: { type: null, required: false },
});

const durationInSeconds = computed(() => `${props.duration}s`);
const animWidth = computed(() => `${getWidth(props.animationType)}%`);
const colorType1 = computed(() => props.color1);
const colorType2 = computed(() => props.color2);

function getWidth(animationType) {
  switch (animationType) {
    case 'none':
      return 12;
    case 'half':
      return 50;
    case 'full':
      return 100;
  }
}
</script>

<style scoped>
.neon-border-container {
  position: relative;
  display: inline-block;
  padding: 2rem;
}

.neon-border-one {
  position: absolute;
  overflow: hidden;
  width: 100%;
  height: 100%;
  filter: blur(1px) drop-shadow(0 0 12px v-bind(colorType1));
  z-index: -1;
  inset: 0;
}

.neon-border-one::before {
  content: "";
  position: absolute;
  overflow: hidden;
  top: 0;
  left: 0;
  width: v-bind(animWidth);
  height: 100%;
  background: linear-gradient(
    135deg,
    v-bind(colorType1),
    v-bind(colorType1),
    transparent,
    transparent
  );
}

.neon-border-two {
  position: absolute;
  overflow: hidden;
  width: 100%;
  height: 100%;
  filter: blur(1px) drop-shadow(0 0 12px v-bind(colorType2));
  z-index: -1;
  inset: 0;
}
.neon-border-two::before {
  content: "";
  position: absolute;
  bottom: 0%;
  right: 0%;
  overflow: hidden;
  width: v-bind(animWidth);
  height: 100%;
  background: linear-gradient(
    135deg,
    transparent,
    transparent,
    v-bind(colorType2),
    v-bind(colorType2)
  );
}

.animate-border {
  animation: rotate v-bind(durationInSeconds) linear infinite;
}

@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>

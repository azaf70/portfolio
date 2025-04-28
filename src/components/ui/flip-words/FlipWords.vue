<template>
  <div class="relative inline-block px-2">
    <Transition @after-enter="$emit('animationStart')" @after-leave="$emit('animationComplete')">
      <div
        v-show="isVisible"
        :class="['relative z-10 inline-block text-center text-white', props.class]"
      >
        <template v-for="(wordObj, wordIndex) in splitWords" :key="wordObj.word + wordIndex">
          <span
            :style="{
              animation: `fadeInWord 0.4s cubic-bezier(0.4, 0, 0.2, 1) forwards`,
              animationDelay: `${wordIndex * 0.2}s`,
            }"
            class="inline-block whitespace-nowrap opacity-0"
          >
            <span
              v-for="(letter, letterIndex) in wordObj.letters"
              :key="wordObj.word + letterIndex"
              :style="{
                animation: `fadeInLetter 0.3s cubic-bezier(0.4, 0, 0.2, 1) forwards`,
                animationDelay: `${wordIndex * 0.2 + letterIndex * 0.03}s`,
              }"
              class="opacity-0 inline-block"
            >
              {{ letter }}
            </span>
            <span class="inline-block">&nbsp;</span>
          </span>
        </template>
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { computed, onBeforeUnmount, onMounted, ref, watch } from 'vue'

const props = defineProps({
  words: { type: Array, required: true },
  duration: { type: Number, required: false, default: 3000 },
  class: { type: String, required: false, default: '' },
})

defineEmits(['animationStart', 'animationComplete'])

const currentWord = ref(props.words[0])
const isVisible = ref(true)
const timeoutId = ref(null)

function startAnimation() {
  isVisible.value = false

  setTimeout(() => {
    const currentIndex = props.words.indexOf(currentWord.value)
    const nextWord = props.words[currentIndex + 1] || props.words[0]
    currentWord.value = nextWord
    isVisible.value = true
  }, 800)
}

const splitWords = computed(() => {
  return currentWord.value.split(' ').map((word) => ({
    word,
    letters: word.split(''),
  }))
})

function startTimeout() {
  timeoutId.value = window.setTimeout(() => {
    startAnimation()
  }, props.duration)
}

onMounted(() => {
  startTimeout()
})

onBeforeUnmount(() => {
  if (timeoutId.value) {
    clearTimeout(timeoutId.value)
  }
})

watch(isVisible, (newValue) => {
  if (newValue) {
    startTimeout()
  }
})
</script>

<style>
@keyframes fadeInWord {
  0% {
    opacity: 0;
    transform: translateY(5px);
    filter: blur(4px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }
}

@keyframes fadeInLetter {
  0% {
    opacity: 0;
    transform: translateY(3px);
    filter: blur(2px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }
}

.v-enter-active {
  animation: enterWord 0.8s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}

.v-leave-active {
  animation: leaveWord 0.8s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}

@keyframes enterWord {
  0% {
    opacity: 0;
    transform: translateY(5px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes leaveWord {
  0% {
    opacity: 1;
    transform: scale(1);
    filter: blur(0);
  }
  100% {
    opacity: 0;
    transform: scale(1.2);
    filter: blur(4px);
  }
}
</style>

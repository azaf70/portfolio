<script setup>
defineProps({
  subtitle: {
    type: String,
    default: '',
  },
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    default: '',
  },
})
</script>

<template>
  <main
    id="content"
    class="relative max-w-6xl px-4 sm:px-6 lg:px-8 flex flex-col justify-center sm:items-center mx-auto"
  >
    <div class="text-center py-8 px-4 sm:px-6 lg:px-8">
      <h2 class="mt-1 sm:mt-3 text-4xl font-bold text-white sm:text-6xl">
        <span class="bg-gradient-to-tr from-[#00cea8] to-[#bf61ff] bg-clip-text text-transparent">
          {{ title }}
        </span>
      </h2>
      <h1 class="text-white font-black md:text-[60px] sm:text-[50px] xs:text-[40px] text-[30px]">
        {{ subtitle }}
      </h1>
      <p class="text-white/80 mx-auto text-md sm:text-xl">
        {{ description }}
      </p>
    </div>
  </main>
</template>

<style scoped></style>

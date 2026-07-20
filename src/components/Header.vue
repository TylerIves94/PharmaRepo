<template>
  <header class="w-full bg-teal-50 border border-teal-100 p-1">
    <h1 class="text-base text-center font-bold text-slate-900">
      Bespoke Pharmacist-led medication reviews
    </h1>
    <button
      @click="emit('open-license')"
      class="w-full p-1 bg-teal-700 hover:bg-teal-800 transition-colors cursor-pointer"
    >
      <p class="text-center text-sm font-semibold text-white underline underline-offset-2">
        Licensed in Wisconsin
      </p>
    </button>
  </header>
</template>

<script setup>
const emit = defineEmits(["open-license"]);
</script>

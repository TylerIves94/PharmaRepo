<template>
  <header class="w-full bg-teal-50 border border-teal-100">
    <div
      class="max-w-6xl mx-auto flex flex-col md:flex-row md:items-center md:justify-between gap-1 md:gap-4 p-1 md:px-8 md:py-4"
    >
      <h1 class="text-base md:text-xl text-center md:text-left font-bold text-slate-900">
        Bespoke Pharmacist-led medication reviews
      </h1>
      <button
        @click="emit('open-license')"
        class="w-full md:w-auto p-1 md:px-4 md:py-1.5 bg-teal-700 hover:bg-teal-800 transition-colors cursor-pointer md:rounded-full md:flex-shrink-0"
      >
        <p
          class="text-center text-sm font-semibold text-white underline underline-offset-2 md:no-underline"
        >
          Licensed in Wisconsin
        </p>
      </button>
    </div>
  </header>
</template>

<script setup>
const emit = defineEmits(["open-license"]);
</script>

<script setup>
import heroImageUrl from "@/assets/backgroundHero.jpg";
</script>

<template>
  <div
    class="relative w-full min-h-[800px] flex items-center justify-center overflow-hidden font-sans p-4"
  >
    <div
      class="absolute inset-0 bg-cover bg-center bg-no-repeat"
      :style="{ backgroundImage: `url(${heroImageUrl})` }"
    ></div>
    <div class="absolute inset-0 bg-black/30"></div>

    <div
      class="relative z-10 max-w-2xl w-full bg-white/60 backdrop-blur-md p-8 md:p-12 rounded-3xl shadow-2xl text-center border border-black"
    >
      <span
        class="inline-block py-1.5 px-4 mb-6 text-xs font-bold tracking-widest text-blue-700 uppercase bg-blue-50 rounded-full border border-blue-100"
      >
        Personalized Care
      </span>
      <h1
        class="text-4xl md:text-5xl font-extrabold text-slate-900 tracking-tight leading-[1.1]"
      >
        One-to-One Extensive <br />
        <span class="text-blue-600">medication reviews</span>
      </h1>
      <p class="mt-6 text-lg md:text-xl text-black font-medium leading-relaxed">
        Get personalized advice and recommendations directly from professionals.
      </p>
      <p class="mt-4 text-md text-red-600 font-semibold">
        Stop stressing over WebMD searches
      </p>
      <div class="mt-10">
        <button
          class="w-full md:w-auto px-12 py-4 bg-blue-600 hover:bg-blue-700 text-white font-bold text-lg rounded-xl transition-all shadow-lg hover:shadow-blue-200"
        >
          Learn more
        </button>
      </div>
    </div>
  </div>
</template>

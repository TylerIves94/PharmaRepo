<script setup>
import heroImageUrl from "@/assets/backgroundHero.jpg";
</script>

<template>
  <div
    class="relative w-full min-h-[600px] md:min-h-[800px] flex items-center justify-center overflow-hidden font-sans p-4"
  >
    <div
      class="absolute inset-0 bg-cover bg-center bg-no-repeat"
      :style="{ backgroundImage: `url(${heroImageUrl})` }"
    ></div>
    <div class="absolute inset-0 bg-black/30"></div>

    <div
      class="relative z-10 max-w-2xl lg:max-w-3xl w-full bg-white/70 backdrop-blur-md p-8 md:p-12 lg:p-16 rounded-3xl shadow-2xl text-center border border-white/40"
    >
      <span
        class="inline-block py-1.5 px-4 mb-6 text-xs font-bold tracking-widest text-teal-700 uppercase bg-teal-50 rounded-full border border-teal-100"
      >
        Personalized Care
      </span>
      <h1
        class="text-4xl md:text-5xl lg:text-6xl font-extrabold text-slate-900 tracking-tight leading-[1.1]"
      >
        One-to-One Extensive <br />
        <span class="text-teal-600">medication reviews</span>
      </h1>
      <p class="mt-6 text-lg md:text-xl lg:text-2xl text-slate-800 font-medium leading-relaxed">
        Get personalized advice and recommendations directly from professionals.
      </p>
      <p class="mt-4 mb-2 text-md lg:text-lg text-amber-600 font-semibold">
        Stop stressing over WebMD searches
      </p>
    </div>
  </div>
</template>

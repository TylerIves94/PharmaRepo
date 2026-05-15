<template>
  <!-- min-h-screen covers the whole page, flex-col keeps items stacked -->

  <div
    class="min-h-screen bg-slate-800 text-slate-900 font-sans flex flex-col items-center"
  >
    <!-- Header: mx-auto + w-full for centering -->
    <header class="w-full bg-blue-300 border border-black p-2">
      <h1 class="text-xl text-center font-bold">
        Bespoke Pharmacist-led medication reviews
      </h1>
      <div class="w-full border border-black mt-2 p-2 bg-black">
        <p class="text-center text-xl font-semibold text-slate-200">
          Licensed in Wisconsin
        </p>
      </div>
    </header>

    <div
      class="relative w-full min-h-[800px] flex items-center justify-center overflow-hidden font-sans p-4"
    >
      <!-- 1. Background Layer: Full opacity but we will use an overlay -->
      <div
        class="absolute inset-0 bg-cover bg-center bg-no-repeat"
        :style="{ backgroundImage: `url(${heroImageUrl})` }"
      ></div>

      <!-- 2. Dark Overlay: This helps the white "card" pop -->
      <div class="absolute inset-0 bg-black/30"></div>

      <!-- 3. The Content Card: Glassmorphism effect -->
      <!-- bg-white/80 adds transparency, backdrop-blur makes the background image non-distracting -->
      <div
        class="relative z-10 max-w-2xl w-full bg-white/60 backdrop-blur-md p-8 md:p-12 rounded-3xl shadow-2xl text-center border border-black"
      >
        <!-- Tagline -->
        <span
          class="inline-block py-1.5 px-4 mb-6 text-xs font-bold tracking-widest text-blue-700 uppercase bg-blue-50 rounded-full border border-blue-100"
        >
          Personalized Care
        </span>

        <!-- Main Headline: Balanced contrast -->
        <h1
          class="text-4xl md:text-5xl font-extrabold text-slate-900 tracking-tight leading-[1.1]"
        >
          One-to-One Extensive <br />
          <span class="text-blue-600">medication reviews</span>
        </h1>

        <!-- Description: High contrast slate color -->
        <p
          class="mt-6 text-lg md:text-xl text-slate-600 font-medium leading-relaxed"
        >
          Get personalized advice and recommendations directly from
          professionals.
        </p>

        <!-- WebMD line: Subtle but distinct -->
        <p class="mt-4 text-md text-red-600 font-semibold">
          Stop stressing over WebMD searches
        </p>

        <!-- Button: Solid color for maximum visibility -->
        <div class="mt-10">
          <button
            class="w-full md:w-auto px-12 py-4 bg-blue-600 hover:bg-blue-700 text-white font-bold text-lg rounded-xl transition-all shadow-lg hover:shadow-blue-200"
          >
            Learn more
          </button>
        </div>
      </div>
    </div>
    <!-- Main Content Container -->
    <div
      ref="targetElement"
      :class="[
        'w-full transition-all duration-2000 transform',
        isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10',
      ]"
    >
      <main class="w-full max-w-2xl p-4 flex flex-col gap-2 bg-slate-900">
        <!-- Top Card (Red) -->
        <div
          class="w-[95%] self-start bg-red-200 rounded-xl border border-black p-4"
        >
          <p class="text-left font-semibold mb-2">What do we offer?</p>
          <p class="text-blue-700 text-right font-semibold">
            A simple way to get answers for all your medication related
            concerns!
          </p>
        </div>

        <!-- Bottom Card (Blue) -->
        <div
          class="w-[95%] self-end bg-blue-200 rounded-xl border border-black p-4"
        >
          <p class="text-left font-semibold mb-2">
            What kind of questions can you answer?
          </p>
          <p class="text-blue-800 text-right font-semibold">
            We are focused on answering every concern you may have, providing a
            bespoke personalized medication and life-style review to help inform
            future decisions.
          </p>
        </div>
        <div
          class="w-[95%] self-start bg-red-200 rounded-xl border border-black p-4"
        >
          <p class="text-left font-semibold mb-2">
            What is the benefit, I already see a doctor?
          </p>
          <p class="text-blue-800 text-right font-semibold">
            We do not work to KPI Targets to line the pockets of a rich CEO, so
            we are able to take as much time as needed to fully review every
            element of the health report that you submit.
          </p>
        </div>
        <div
          class="w-[95%] self-end bg-blue-200 rounded-xl border border-black p-4"
        >
          <p class="text-left font-semibold mb-2">
            What kind of questions can you answer?
          </p>
          <p class="text-blue-800 text-right font-semibold">
            We are focused on answering every concern you may have, providing a
            bespoke personalized medication and life-style review to help inform
            future decisions.
          </p>
        </div>
      </main>
    </div>

    <div class="bg-red-200 w-full">
      <p class="text-center text-lg font-semibold outline-1">
        What is this service?
      </p>
    </div>
    <div>
      <p class="text-md p-2 bg-slate-200 m-2 rounded-lg">
        Regular doctors and pharmacists do all they can in the hope of helping
        you, the client, but they are all limited by their involvement with Big
        Pharma, putting profit and efficiency above all else.
        <span class="font-semibold text-blue-800"
          >This leads to treating people like numbers on a conveyer belt.
        </span>
      </p>
      <p class="text-md p-2 bg-slate-200 m-2 rounded-lg">
        This service offers extensive one-on-one consultations to analyzes all
        the medications (Prescribed, Over-the-counter-vitamins and supplements)
        to check for interactions, reduce waste, ensuring dosages line up,
        managing possible or ongoing side effects and creating a personalized
        medication action plan!
      </p>
    </div>
  </div>
</template>

<script setup>
// 1. Import the image so Vite can process it and provide the correct URL
import heroImageUrl from "@/assets/backgroundHero.jpg";
import { ref, onMounted, onUnmounted } from "vue";

const targetElement = ref(null);
const isVisible = ref(false);

// Logic for the observer
let observer = null;

onMounted(() => {
  const options = {
    root: null, // use the viewport
    threshold: 0.2, // trigger when 20% of the element is visible
  };

  observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        isVisible.value = true;
        // If you only want it to appear once, unobserve here
        observer.unobserve(entry.target);
      }
    });
  }, options);

  if (targetElement.value) {
    observer.observe(targetElement.value);
  }
});

onUnmounted(() => {
  if (observer) observer.disconnect();
});
</script>

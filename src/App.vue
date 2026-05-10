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
      class="relative w-full min-h-[800px] flex items-center justify-center overflow-hidden"
    >
      <!-- 2. The Background Layer: Absolute, fills the parent, and has the opacity -->
      <div
        class="absolute inset-0 bg-cover bg-center bg-no-repeat opacity-60"
        :style="{ backgroundImage: `url(${heroImageUrl})` }"
      ></div>

      <!-- 3. The Content Layer: Must be 'relative' to sit on top of the background -->
      <div class="relative z-10 p-6 flex-1">
        <p
          class="p-2 text-4xl text-center font-bold text-blue-800 drop-shadow-sm"
        >
          One-To-One Extensive medication reviews
        </p>
        <p
          class="p-2 text-4xl text-center font-bold text-red-800 drop-shadow-sm"
        >
          Don't stress yourself out on webMD
        </p>
        <p class="p-2 text-4xl text-center font-bold text-white drop-shadow-sm">
          Get personalized advice and recommendations directly from
          professionals!
        </p>
        <div class="w-full justify-center items-center text-center">
          <button
            class="p-4 mt-8 bg-black text-white font-bold text-3xl text-center rounded-4xl px-20 outline-3"
          >
            Learn more!
          </button>
        </div>
      </div>
    </div>

    <!-- Main Content Container -->
    <main class="w-full max-w-2xl p-4 flex flex-col gap-2">
      <!-- Top Card (Red) -->
      <div
        class="w-[95%] self-start bg-red-200 rounded-xl border border-black p-4"
      >
        <p class="text-left text-lg font-semibold mb-2">What do we offer?</p>
        <p class="text-lg text-blue-700 text-right font-semibold">
          A simple way to get answers for all your medication related concerns!
        </p>
      </div>

      <!-- Bottom Card (Blue) -->
      <div
        class="w-[95%] self-end bg-blue-200 rounded-xl border border-black p-4"
      >
        <p class="text-left text-lg font-semibold mb-2">
          What kind of questions can you answer?
        </p>
        <p class="text-lg text-blue-800 text-right font-semibold">
          We are focused on answering every concern you may have, providing a
          bespoke personalized medication and life-style review to help inform
          future decisions.
        </p>
      </div>
      <div
        class="w-[95%] self-start bg-red-200 rounded-xl border border-black p-4"
      >
        <p class="text-left text-lg font-semibold mb-2">
          What is the benefit, I already see a doctor?
        </p>
        <p class="text-lg text-blue-800 text-right font-semibold">
          We do not work to KPI Targets to line the pockets of a rich CEO, so we
          are able to take as much time as needed to fully review every element
          of the health report that you submit.
        </p>
      </div>
    </main>
    <div
      ref="targetElement"
      :class="[
        'w-full transition-all duration-2000 transform',
        isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10',
      ]"
    >
      <div class="bg-red-200">
        <p class="text-center text-lg font-semibold outline-1">
          What is this service?
        </p>
      </div>
      <div>
        <p class="text-md p-2 bg-slate-200 m-2 rounded-lg">
          Regular doctors and pharmacists do all they can in the hope of helping
          you, the client, but they are all limited by their involvement with
          Big Pharma, putting profit and efficiency above all else.
          <span class="font-semibold text-blue-800"
            >This leads to treating people like numbers on a conveyer belt.
          </span>
        </p>
        <p class="text-md p-2 bg-slate-200 m-2 rounded-lg">
          This service offers extensive one-on-one consultations to analyzes all
          the medications (Prescribed, Over-the-counter-vitamins and
          supplements) to check for interactions, reduce waste, ensuring dosages
          line up, managing possible or ongoing side effects and creating a
          personalized medication action plan!
        </p>
      </div>
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

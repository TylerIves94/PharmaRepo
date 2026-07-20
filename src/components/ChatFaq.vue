<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const targetElement = ref(null);
const isVisible = ref(false);
const isExpanded = ref(false);
let observer = null;

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          isVisible.value = true;
          observer.unobserve(entry.target);
        }
      });
    },
    { threshold: 0.2 },
  );

  if (targetElement.value) observer.observe(targetElement.value);
});

onUnmounted(() => {
  if (observer) observer.disconnect();
});
</script>
<template>
  <div
    ref="targetElement"
    :class="[
      'w-full transition-all duration-700 ease-out transform flex flex-col items-center',
      isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10',
    ]"
  >
    <main
      class="w-full p-4 flex flex-col gap-6 bg-gradient-to-tr from-slate-900 via-teal-950 to-slate-900 rounded-b-3xl relative border-b border-white/10 overflow-hidden"
    >
      <p class="text-center text-white font-semibold text-xl">
        Got questions? We've got answers!
      </p>

      <div
        class="w-[85%] self-start bg-white rounded-2xl rounded-tl-none p-5 shadow-lg border-l-4 border-teal-500"
      >
        <p class="text-slate-900 font-bold text-lg mb-2">What do we offer?</p>
        <p class="text-slate-600 leading-relaxed">
          A simple way to get answers for all your medication related concerns!
        </p>
      </div>

      <div class="w-[85%] self-end relative">
        <div
          class="bg-teal-600 rounded-2xl rounded-tr-none p-5 shadow-xl text-white border-r-4 border-white"
        >
          <p class="font-bold text-lg mb-2">
            What kind of questions can you answer?
          </p>
          <p class="text-teal-50 leading-relaxed">
            We are focused on answering every concern you may have, providing a
            bespoke personalized medication review.
          </p>
        </div>

        <div
          v-if="!isExpanded"
          class="absolute inset-x-0 bottom-0 h-24 bg-gradient-to-t from-slate-900 to-transparent pointer-events-none"
        ></div>
      </div>

      <div
        class="flex flex-col gap-6 overflow-hidden transition-all duration-700 ease-in-out"
        :style="{
          maxHeight: isExpanded ? '2000px' : '0px',
          opacity: isExpanded ? '1' : '0',
        }"
      >
        <div
          class="w-[85%] self-start bg-white rounded-2xl rounded-tl-none p-5 shadow-lg border-l-4 border-teal-500"
        >
          <p class="text-slate-900 font-bold text-lg mb-2">
            What is the benefit? I already see a doctor.
          </p>
          <p class="text-slate-600 leading-relaxed">
            We do not work to KPI Targets. We take as much time as needed to
            fully review every element of your health report.
          </p>
        </div>

        <div
          class="w-[85%] self-end bg-teal-600 rounded-2xl rounded-tr-none p-5 shadow-xl text-white border-r-4 border-white"
        >
          <p class="font-bold text-lg mb-2">Something else on your mind?</p>
          <p class="text-teal-50 leading-relaxed">
            Reach out via the enquiry form below—we're happy to answer
            anything not covered here.
          </p>
        </div>

        <div
          class="w-[85%] self-start bg-white rounded-2xl rounded-tl-none p-5 shadow-lg border-l-4 border-teal-500"
        >
          <p class="text-slate-900 font-bold text-lg mb-2">Is my data safe?</p>
          <p class="text-slate-600 leading-relaxed">
            Yes, we follow all HIPAA guidelines to ensure your privacy.
          </p>
        </div>

        <div
          class="w-[85%] self-end bg-teal-600 rounded-2xl rounded-tr-none p-5 shadow-xl text-white border-r-4 border-white"
        >
          <p class="font-bold text-lg mb-2">Can I do this from home?</p>
          <p class="text-teal-50 leading-relaxed">
            Absolutely, our pharmacist reviews can be handled entirely via
            secure video or phone call.
          </p>
        </div>
      </div>

      <div class="flex justify-center mt-4">
        <button
          @click="isExpanded = !isExpanded"
          class="group flex items-center gap-2 px-6 py-2 bg-slate-800 hover:bg-slate-700 text-teal-400 font-bold rounded-full border border-slate-700 transition-all shadow-md"
        >
          <span>{{ isExpanded ? "Show less" : "View more questions" }}</span>
          <svg
            :class="{ 'rotate-180': isExpanded }"
            class="w-4 h-4 transition-transform duration-300"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="3"
              d="M19 9l-7 7-7-7"
            />
          </svg>
        </button>
      </div>
    </main>
  </div>
</template>

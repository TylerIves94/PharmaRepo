<script setup>
import { Send, PhoneCall, Users, Compass } from "lucide-vue-next";

const steps = [
  {
    icon: Send,
    title: "Reach out",
    detail:
      "Send a quick message with your name and what's going on. Two minutes, and it's free to ask.",
  },
  {
    icon: PhoneCall,
    title: "We call you back",
    detail: "Usually within a day, to find a time that actually works for you.",
  },
  {
    icon: Users,
    title: "Have a real conversation",
    detail:
      "30–45 minutes, by phone or video—also free. Grab your pill bottles, or just a list of what you're taking.",
  },
  {
    icon: Compass,
    title: "Know what's next",
    detail:
      "By the end of the call, you'll know exactly how we can help. No pressure, no hard sell.",
  },
];
</script>

<template>
  <div
    class="w-full bg-white py-8 lg:py-16 px-4 lg:px-8 flex flex-col items-center"
  >
    <div class="max-w-2xl w-full mb-12 text-center">
      <h2 class="text-2xl md:text-3xl lg:text-4xl font-extrabold text-slate-900">
        What to <span class="text-teal-600">Expect</span>
      </h2>
      <p class="mt-3 text-slate-600 max-w-md mx-auto">
        Your first consultation is completely free. Here's what actually
        happens.
      </p>
    </div>

    <div class="max-w-2xl lg:max-w-5xl w-full relative">
      <div
        class="absolute left-6 top-4 bottom-4 w-0.5 bg-teal-100 lg:hidden"
      ></div>
      <div
        class="hidden lg:block absolute top-6 left-[12.5%] right-[12.5%] h-0.5 bg-teal-100"
      ></div>

      <div class="flex flex-col gap-10 lg:flex-row lg:gap-6">
        <div
          v-for="step in steps"
          :key="step.title"
          class="relative flex gap-5 lg:flex-1 lg:flex-col lg:items-center lg:text-center lg:gap-4"
        >
          <div
            class="relative z-10 flex-shrink-0 w-12 h-12 rounded-full bg-teal-600 flex items-center justify-center text-white shadow-md"
          >
            <component :is="step.icon" class="w-5 h-5" />
          </div>
          <div class="lg:max-w-[220px]">
            <h3 class="font-bold text-slate-900 mb-1">{{ step.title }}</h3>
            <p class="text-sm text-slate-600 leading-relaxed">
              {{ step.detail }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

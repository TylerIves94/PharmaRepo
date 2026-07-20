<script setup>
defineProps({
  isOpen: Boolean,
});

const emit = defineEmits(["close"]);

// Filler staff details — replace with real team info before launch.
const staff = [
  {
    name: "Jane Doe, PharmD",
    role: "Lead Clinical Pharmacist",
    license: "License #: Pending",
  },
  {
    name: "John Smith, PharmD, BCACP",
    role: "Clinical Pharmacist",
    license: "License #: Pending",
  },
];
</script>

<template>
  <div
    v-if="isOpen"
    class="fixed inset-0 z-50 flex items-center justify-center p-2 bg-slate-900/60 backdrop-blur-sm"
    @click.self="emit('close')"
  >
    <div
      class="relative max-w-2xl w-full bg-slate-50 rounded-2xl shadow-2xl overflow-hidden border border-slate-200 animate-in fade-in zoom-in duration-300 max-h-[90vh] flex flex-col"
    >
      <button
        @click="emit('close')"
        class="absolute top-4 right-4 text-white hover:scale-110 transition-transform z-10"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-8 w-8"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M6 18L18 6M6 6l12 12"
          />
        </svg>
      </button>

      <div class="overflow-y-auto flex-1 min-h-0">
        <div
          class="bg-gradient-to-r from-teal-600 to-teal-800 p-8 text-center text-white"
        >
          <h2 class="text-3xl font-extrabold">Licensing &amp; Credentials</h2>
          <p class="text-teal-100 mt-2 font-medium">
            Meet the team behind your reviews
          </p>
        </div>

        <div class="p-8 md:p-12 space-y-6 bg-slate-50">
          <p class="text-slate-700 leading-relaxed">
            Every medication review is conducted exclusively by pharmacists
            licensed by the
            <strong>Wisconsin Pharmacy Examining Board</strong>. Each member
            of our clinical team holds an active, unrestricted license in
            good standing and is qualified to review prescriptions,
            over-the-counter medications, vitamins, and supplements.
          </p>

          <div>
            <h3
              class="text-xs font-bold uppercase tracking-widest text-slate-500 mb-3"
            >
              Our Licensed Pharmacists
            </h3>
            <div class="space-y-3">
              <div
                v-for="member in staff"
                :key="member.name"
                class="bg-white p-4 rounded-xl border border-slate-200 shadow-sm"
              >
                <p class="font-bold text-slate-900">{{ member.name }}</p>
                <p class="text-sm text-slate-600">{{ member.role }}</p>
                <p class="text-xs text-teal-700 font-semibold mt-1">
                  {{ member.license }}
                </p>
              </div>
            </div>
          </div>

          <div
            class="bg-slate-100 p-4 rounded-lg border border-teal-300 text-slate-600"
          >
            <h4
              class="text-xs font-bold uppercase tracking-wider text-slate-500 mb-1"
            >
              Disclaimer
            </h4>
            <p class="text-[11px] leading-relaxed">
              This service is licensed to operate in the State of Wisconsin
              only. Reviews are provided for
              <strong>informational and educational purposes only</strong>
              and do not constitute a guarantee of health outcomes or medical
              results. This service is not a replacement for emergency
              medical care. Always consult your primary care physician
              before making any changes to prescribed medication.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

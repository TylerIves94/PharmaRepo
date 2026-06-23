<script setup>
import { reactive } from "vue";
import BaseInput from "./BaseInput.vue";

defineProps({
  isOpen: Boolean,
});

const emit = defineEmits(["close"]);

const form = reactive({
  name: "",
  email: "",
  phone: "",
  message: "",
  toggle: "self",
  reachOutSubject: "", // For the first question
  historyKnowledge: "", // For the second question
});

const handleFormSubmit = () => {
  console.log("Form Submitted:", form);
  alert("Thank you! Your enquiry has been sent.");
  Object.keys(form).forEach((key) => (form[key] = ""));
  // Need to add functionality to send completed form details to email, and save a copy within database
  // T.I 19/06/2026

  // Must ensure HIPAA Compliance is followed (As much as possible for a personal project currently) TI

  emit("close");
};
</script>

<template>
  <div
    v-if="isOpen"
    class="fixed inset-0 z-50 flex items-center justify-center p-2 bg-slate-900/60 backdrop-blur-sm"
    @click.self="emit('close')"
  >
    <div
      class="relative max-w-3xl w-full bg-slate-50 rounded-2xl shadow-2xl overflow-hidden border border-slate-200 animate-in fade-in zoom-in duration-300 max-h-[110vh] overflow-y-auto"
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

      <div
        class="bg-gradient-to-r from-blue-600 to-indigo-700 p-8 text-center text-white"
      >
        <h2 class="text-3xl font-extrabold">Start Your Review</h2>
        <p class="text-blue-100 mt-2 font-medium">
          We need just a few details to get started
        </p>
      </div>

      <form
        @submit.prevent="handleFormSubmit"
        class="p-8 md:p-12 space-y-6 bg-slate-50"
      >
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <BaseInput
            label="Full Name"
            v-model="form.name"
            placeholder="John Doe"
            required
          />
          <BaseInput
            label="Email Address"
            v-model="form.email"
            type="email"
            placeholder="john@example.com"
            required
          />
        </div>

        <BaseInput
          label="Are You Reaching out for yourself or a loved one?"
          v-model="form.reachOutSubject"
          name="reachOutSubject"
          type="radio"
          :options="[
            { label: 'Myself', value: 'self' },
            { label: 'Someone Else', value: 'someone_else' },
          ]"
          required
        />

        <BaseInput
          label="Are you familiar with {USER} medical history?"
          v-model="form.historyKnowledge"
          name="historyKnowledge"
          type="radio"
          :options="[
            { label: 'Very', value: 'very' },
            { label: 'Somewhat', value: 'somewhat' },
            { label: 'Minimal Info', value: 'minimal_info' },
          ]"
        />

        <BaseInput
          label="Other Notes?"
          v-model="form.message"
          type="textarea"
          optional
        />

        <div
          class="bg-slate-100 p-4 rounded-lg border-1 border-blue-400 text-slate-600"
        >
          <h4
            class="text-xs font-bold uppercase tracking-wider text-slate-500 mb-1"
          >
            Disclaimer & Terms
          </h4>
          <p class="text-[11px] leading-relaxed">
            By submitting this form, you acknowledge that this consultation is
            for
            <strong>informational and educational purposes only</strong>. While
            our reviews are conducted by licensed pharmacists, the advice
            provided does not constitute a guarantee of health outcomes or
            medical results. This service is not a replacement for emergency
            medical care. Always consult your primary care physician before
            making any changes to prescribed medication.
          </p>
        </div>

        <button
          type="submit"
          class="w-full py-4 bg-blue-600 hover:bg-blue-700 text-white font-bold rounded-xl transition-all shadow-lg shadow-blue-200"
        >
          Submit Enquiry
        </button>
      </form>
    </div>
  </div>
</template>

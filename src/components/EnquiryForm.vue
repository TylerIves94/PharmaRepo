<script setup>
import { reactive, ref, computed } from "vue";
import BaseInput from "./BaseInput.vue";

defineProps({
  isOpen: Boolean,
});

const emit = defineEmits(["close"]);

const FORM_ENDPOINT = "https://formspree.io/f/xpqvrneq";

const createFormState = () => ({
  name: "",
  email: "",
  phone: "",
  message: "",
  toggle: "self",
  reachOutSubject: "self",
  historyKnowledge: "",
});

const form = reactive(createFormState());

// idle | submitting | success | error
// This form intentionally collects only contact/screening info, not
// clinical details, so relaying it via Formspree to a staff inbox is
// fine — real medical history is handled securely during the consult.
const status = ref("idle");

const subjectPronoun = computed(() =>
  form.reachOutSubject === "someone_else" ? "their" : "your",
);

const handleFormSubmit = async () => {
  status.value = "submitting";
  try {
    const response = await fetch(FORM_ENDPOINT, {
      method: "POST",
      headers: {
        Accept: "application/json",
        "Content-Type": "application/json",
      },
      body: JSON.stringify(form),
    });

    if (!response.ok) throw new Error("Submission failed");

    status.value = "success";
    Object.assign(form, createFormState());
  } catch (err) {
    status.value = "error";
  }
};

const handleClose = () => {
  status.value = "idle";
  emit("close");
};
</script>

<template>
  <div
    v-if="isOpen"
    class="fixed inset-0 z-50 flex items-center justify-center p-2 bg-slate-900/60 backdrop-blur-sm"
    @click.self="handleClose"
  >
    <div
      class="relative max-w-3xl w-full bg-slate-50 rounded-2xl shadow-2xl overflow-hidden border border-slate-200 animate-in fade-in zoom-in duration-300 max-h-[90vh] flex flex-col"
    >
      <button
        @click="handleClose"
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
          <h2 class="text-3xl font-extrabold">Start Your Review</h2>
          <p class="text-teal-100 mt-2 font-medium">
            We need just a few details to get started
          </p>
        </div>

        <div
          v-if="status === 'success'"
          class="p-8 md:p-12 text-center space-y-4"
        >
          <div
            class="mx-auto w-14 h-14 rounded-full bg-teal-100 flex items-center justify-center"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-7 w-7 text-teal-600"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 13l4 4L19 7"
              />
            </svg>
          </div>
          <h3 class="text-xl font-bold text-slate-900">
            Thanks — we've got it!
          </h3>
          <p class="text-slate-600 leading-relaxed">
            Your enquiry has been sent to our team. We'll be in touch soon at
            the email you provided.
          </p>
          <button
            @click="handleClose"
            class="w-full py-3 bg-teal-600 hover:bg-teal-700 text-white font-bold rounded-xl transition-all"
          >
            Close
          </button>
        </div>

        <form
          v-else
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
          :label="`Are you familiar with ${subjectPronoun} medical history?`"
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
          label="Anything else we should know before reaching out? (Please don't include specific medical details here—we'll cover that securely during your consultation.)"
          v-model="form.message"
          type="textarea"
          optional
        />

        <div
          class="bg-slate-100 p-4 rounded-lg border border-teal-300 text-slate-600"
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

          <p v-if="status === 'error'" class="text-red-600 text-sm font-medium">
            Something went wrong sending your enquiry. Please try again.
          </p>

          <button
            type="submit"
            :disabled="status === 'submitting'"
            class="w-full py-4 bg-teal-600 hover:bg-teal-700 disabled:opacity-60 disabled:cursor-not-allowed text-white font-bold rounded-xl transition-all shadow-lg shadow-teal-200"
          >
            {{ status === "submitting" ? "Sending…" : "Submit Enquiry" }}
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from "vue";
import BaseInput from "./BaseInput.vue";

const form = reactive({
  name: "",
  email: "",
  phone: "",
  message: "",
});

const handleFormSubmit = () => {
  console.log("Form Submitted:", form);
  alert("Thank you! Your enquiry has been sent.");
  Object.keys(form).forEach((key) => (form[key] = ""));
};
</script>

<template>
  <div
    id="enquiry-form"
    class="w-full bg-slate-50 py-4 px-2 flex flex-col items-center"
  >
    <div
      class="max-w-3xl w-full bg-slate-50 rounded-lg shadow-2xl overflow-hidden border border-black"
    >
      <div
        class="bg-gradient-to-r from-blue-600 to-indigo-700 p-8 text-center text-white"
      >
        <h2 class="text-3xl font-extrabold">Start Your Review</h2>
        <p class="text-blue-100 mt-2 font-medium">
          Fill out the form below and a pharmacist will reach out.
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
          v-model="form.toggle"
          type="radio"
          :options="[
            { label: 'Myself', value: 'self' },
            { label: 'Someone Else', value: 'someone_else' },
          ]"
          required
        />
        <BaseInput
          label="Other Notes?"
          v-model="form.message"
          type="textarea"
          required
        />
        <button
          type="submit"
          class="w-full py-4 bg-blue-600 hover:bg-blue-700 text-white font-bold rounded-xl transition-all"
        >
          Submit Enquiry
        </button>
      </form>
    </div>
  </div>
</template>

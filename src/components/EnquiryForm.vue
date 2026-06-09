<script setup>
import { reactive } from "vue";

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
    class="w-full bg-slate-800 py-8 px-2 flex flex-col items-center"
  >
    <div
      class="max-w-3xl w-full bg-white rounded-[2.5rem] shadow-2xl overflow-hidden border border-white/20"
    >
      <div
        class="bg-gradient-to-r from-blue-600 to-indigo-700 p-8 text-center text-white"
      >
        <h2 class="text-3xl font-extrabold">Start Your Review</h2>
        <p class="text-blue-100 mt-2 font-medium">
          Fill out the form below and a pharmacist will reach out.
        </p>
      </div>

      <form @submit.prevent="handleFormSubmit" class="p-8 md:p-12 space-y-6">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <div class="flex flex-col gap-2">
            <label class="text-sm font-bold text-slate-700 uppercase"
              >Full Name</label
            >
            <input
              v-model="form.name"
              type="text"
              required
              placeholder="John Doe"
              class="input-style"
            />
          </div>
          <div class="flex flex-col gap-2">
            <label class="text-sm font-bold text-slate-700 uppercase"
              >Email Address</label
            >
            <input
              v-model="form.email"
              type="email"
              required
              placeholder="john@example.com"
              class="input-style"
            />
          </div>
        </div>
        <div class="flex flex-col gap-2">
          <label class="text-sm font-bold text-slate-700 uppercase"
            >Message</label
          >
          <textarea
            v-model="form.message"
            rows="4"
            required
            class="input-style"
          ></textarea>
        </div>
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

<style scoped></style>

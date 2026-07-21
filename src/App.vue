<template>
  <div
    class="min-h-screen bg-slate-900 text-slate-900 font-sans flex flex-col items-center"
  >
    <Header @open-license="showLicenseModal = true" />

    <HeroSection />

    <div
      class="w-full relative overflow-hidden bg-gradient-to-b from-slate-50 via-teal-50/40 to-slate-50 py-8 lg:py-16 px-4 lg:px-8 flex flex-col items-center"
    >
      <div
        class="hidden md:block absolute -top-24 -left-24 w-72 h-72 bg-teal-200/50 rounded-full blur-3xl -z-0 pointer-events-none"
      ></div>
      <div
        class="hidden md:block absolute top-1/3 -right-24 w-96 h-96 bg-amber-100/60 rounded-full blur-3xl -z-0 pointer-events-none"
      ></div>

      <div class="max-w-2xl w-full mb-12 text-center relative z-10">
        <h2 class="text-2xl md:text-3xl lg:text-4xl font-extrabold text-slate-900">
          Getting the knowledge you want <br />
          <span class="text-teal-600">has never been easier</span>
        </h2>

        <div class="h-1 w-20 bg-teal-600 mx-auto mt-4 rounded-full"></div>
      </div>

      <div class="max-w-3xl w-full relative z-10 mb-10">
        <div
          class="bg-white rounded-3xl shadow-sm border border-slate-100 p-8 md:p-10 text-center"
        >
          <Quote class="w-8 h-8 text-teal-100 mx-auto mb-3" />
          <p class="text-lg md:text-xl text-slate-700 leading-relaxed max-w-xl mx-auto">
            Regular doctors and pharmacists do all they can to help, but
            they're often limited by corporate targets that put efficiency
            above all else.
          </p>
          <p class="mt-4 text-xl md:text-2xl font-bold text-teal-700 italic">
            "Treated like numbers on a conveyor belt."
          </p>
        </div>
      </div>

      <div
        class="max-w-2xl lg:max-w-4xl w-full grid grid-cols-1 md:grid-cols-2 gap-8 relative z-10"
      >
        <div
          class="flex flex-col items-center text-center md:items-start md:text-left gap-3"
        >
          <div
            class="w-10 h-10 rounded-lg bg-teal-600 flex items-center justify-center text-white flex-shrink-0"
          >
            <Stethoscope class="w-5 h-5" />
          </div>
          <h3 class="font-bold text-slate-900 text-lg">The Consultation</h3>
          <p class="text-slate-600 leading-relaxed">
            We offer extensive
            <strong class="text-slate-900">one-on-one consultations</strong>
            to analyze all your medications—including prescriptions, vitamins,
            and supplements. We check for interactions and ensure your dosages
            line up perfectly.
          </p>
        </div>

        <div
          class="flex flex-col items-center text-center md:items-start md:text-left gap-3 md:border-l md:border-slate-200 md:pl-8"
        >
          <div
            class="w-10 h-10 rounded-lg bg-teal-600 flex items-center justify-center text-white flex-shrink-0"
          >
            <ClipboardCheck class="w-5 h-5" />
          </div>
          <h3 class="font-bold text-slate-900 text-lg">The Action Plan</h3>
          <p class="text-slate-600 leading-relaxed">
            We focus on reducing waste, managing side effects, and creating a
            clear, actionable plan tailored to your unique health needs and
            goals.
          </p>
        </div>
      </div>
    </div>

    <WhatToExpect />

    <div
      class="w-full bg-gradient-to-b from-white to-teal-50 pb-12 lg:pb-20 px-4 flex flex-col items-center"
    >
      <div class="max-w-xl w-full">
        <button
          @click="showEnquiryModal = true"
          class="w-full bg-gradient-to-r from-teal-600 to-teal-800 p-8 rounded-3xl shadow-xl text-center transform hover:scale-[1.02] transition-transform"
        >
          <p class="text-white text-2xl font-bold">
            Click here to
            <span class="text-amber-300 text-3xl">Get Started.</span>
          </p>
        </button>
      </div>
    </div>
    <ChatFaq />
    <EnquiryForm :isOpen="showEnquiryModal" @close="showEnquiryModal = false" />
    <LicenseModal
      :isOpen="showLicenseModal"
      @close="showLicenseModal = false"
    />

    <footer class="w-full bg-slate-900 pt-12 pb-8 px-4 text-slate-400 text-sm">
      <div class="max-w-2xl mx-auto flex flex-col items-center gap-6">
        <div
          class="w-full flex flex-col sm:flex-row sm:justify-center items-center gap-4 sm:gap-8 text-center"
        >
          <!-- Placeholder number (555-01xx is the reserved fictional range) — replace before launch -->
          <a
            href="tel:+16085550100"
            class="flex items-center gap-2 hover:text-white transition-colors"
          >
            <Phone class="w-4 h-4 text-teal-500 flex-shrink-0" />
            (608) 555-0100
          </a>
          <a
            href="mailto:pharmaenquiry@outlook.com"
            class="flex items-center gap-2 hover:text-white transition-colors"
          >
            <Mail class="w-4 h-4 text-teal-500 flex-shrink-0" />
            pharmaenquiry@outlook.com
          </a>
          <span class="flex items-center gap-2">
            <MapPin class="w-4 h-4 text-teal-500 flex-shrink-0" />
            Anywhere in Wisconsin
          </span>
        </div>

        <p
          class="flex items-center gap-2 text-xs text-slate-500 text-center max-w-sm"
        >
          <Clock class="w-4 h-4 text-teal-500 flex-shrink-0" />
          Available by appointment—we aim to respond to all enquiries within
          24 hours.
        </p>

        <div class="w-full h-px bg-slate-800"></div>

        <p class="text-xs text-slate-500 text-center">
          &copy; {{ new Date().getFullYear() }} Pharmacist-Led Medication
          Reviews.
          <button
            @click="showLicenseModal = true"
            class="underline underline-offset-2 hover:text-slate-300 transition-colors cursor-pointer"
          >
            Licensed in Wisconsin.
          </button>
        </p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref } from "vue";
import {
  Phone,
  Mail,
  MapPin,
  Clock,
  Quote,
  Stethoscope,
  ClipboardCheck,
} from "lucide-vue-next";
import Header from "./components/Header.vue";
import HeroSection from "./components/HeroSection.vue";
import ChatFaq from "./components/ChatFaq.vue";
import EnquiryForm from "./components/EnquiryForm.vue";
import LicenseModal from "./components/LicenseModal.vue";
import WhatToExpect from "./components/WhatToExpect.vue";

// Control Viability of Form
const showEnquiryModal = ref(false);
const showLicenseModal = ref(false);
</script>

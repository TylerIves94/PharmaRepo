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
        class="absolute -top-24 -left-24 w-72 h-72 bg-teal-200/50 rounded-full blur-3xl -z-0 pointer-events-none"
      ></div>
      <div
        class="absolute top-1/3 -right-24 w-96 h-96 bg-amber-100/60 rounded-full blur-3xl -z-0 pointer-events-none"
      ></div>

      <div class="max-w-2xl w-full mb-12 text-center relative z-10">
        <h2 class="text-2xl md:text-3xl lg:text-4xl font-extrabold text-slate-900">
          Getting the knowledge you want <br />
          <span class="text-teal-600">has never been easier</span>
        </h2>

        <div class="h-1 w-20 bg-teal-600 mx-auto mt-4 rounded-full"></div>
      </div>

      <div
        class="max-w-2xl lg:max-w-5xl w-full space-y-6 md:space-y-12 lg:space-y-0 lg:grid lg:grid-cols-3 lg:gap-8 relative z-10"
      >
        <div
          class="absolute left-6 top-0 bottom-0 w-0.5 bg-slate-200 z-0 lg:hidden"
        ></div>

        <div class="relative z-10 flex gap-6 lg:flex-col lg:items-center lg:text-center lg:gap-4 group">
          <div
            class="flex-shrink-0 w-12 h-12 rounded-full bg-white border-2 border-teal-600 flex items-center justify-center font-bold text-teal-600 shadow-sm group-hover:bg-teal-600 group-hover:text-white transition-colors"
          >
            1
          </div>
          <div
            class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100 flex-1"
          >
            <h3
              class="flex items-center lg:justify-center gap-2 text-sm font-bold uppercase tracking-widest text-slate-400 mb-2"
            >
              <AlertCircle class="w-4 h-4 text-teal-600 flex-shrink-0" />
              The Problem
            </h3>
            <p class="text-slate-700 leading-relaxed">
              Regular doctors and pharmacists do all they can to help, but they
              are often limited by corporate targets, putting efficiency above
              all else.
              <span class="block mt-2 font-semibold text-teal-700 italic">
                "This often leads to people being treated like numbers on a
                conveyor belt."
              </span>
            </p>
          </div>
        </div>

        <div class="relative z-10 flex gap-6 lg:flex-col lg:items-center lg:text-center lg:gap-4 group">
          <div
            class="flex-shrink-0 w-12 h-12 rounded-full bg-white border-2 border-teal-600 flex items-center justify-center font-bold text-teal-600 shadow-sm group-hover:bg-teal-600 group-hover:text-white transition-colors"
          >
            2
          </div>
          <div
            class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100 flex-1"
          >
            <h3
              class="flex items-center lg:justify-center gap-2 text-sm font-bold uppercase tracking-widest text-slate-400 mb-2"
            >
              <Stethoscope class="w-4 h-4 text-teal-600 flex-shrink-0" />
              The Consultation
            </h3>
            <p class="text-slate-700 leading-relaxed">
              We offer extensive
              <span class="font-bold text-slate-900"
                >one-on-one consultations</span
              >
              to analyze all your medications—including prescriptions, vitamins,
              and supplements. We check for interactions and ensure your dosages
              line up perfectly.
            </p>
          </div>
        </div>
        <div class="relative z-10 flex gap-6 lg:flex-col lg:items-center lg:text-center lg:gap-4 group">
          <div
            class="flex-shrink-0 w-12 h-12 rounded-full bg-white border-2 border-teal-600 flex items-center justify-center font-bold text-teal-600 shadow-sm group-hover:bg-teal-600 group-hover:text-white transition-colors"
          >
            3
          </div>
          <div
            class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100 flex-1"
          >
            <h3
              class="flex items-center lg:justify-center gap-2 text-sm font-bold uppercase tracking-widest text-slate-400 mb-2"
            >
              <ClipboardCheck class="w-4 h-4 text-teal-600 flex-shrink-0" />
              The Action Plan
            </h3>
            <p class="text-slate-700 leading-relaxed">
              We focus on reducing waste, managing side effects, and creating a
              clear, actionable plan tailored to your unique health needs and
              goals.
            </p>
          </div>
        </div>
      </div>
      <div class="h-1 w-20 bg-teal-600 mx-auto mt-8 rounded-full"></div>

      <div class="mt-8 lg:mt-12 max-w-xl w-full relative z-10">
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
  AlertCircle,
  Stethoscope,
  ClipboardCheck,
} from "lucide-vue-next";
import Header from "./components/Header.vue";
import HeroSection from "./components/HeroSection.vue";
import ChatFaq from "./components/ChatFaq.vue";
import EnquiryForm from "./components/EnquiryForm.vue";
import LicenseModal from "./components/LicenseModal.vue";

// Control Viability of Form
const showEnquiryModal = ref(false);
const showLicenseModal = ref(false);
</script>

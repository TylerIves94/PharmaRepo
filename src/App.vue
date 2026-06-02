<template>
  <!-- min-h-screen covers the whole page, flex-col keeps items stacked -->

  <div
    class="min-h-screen bg-slate-800 text-slate-900 font-sans flex flex-col items-center"
  >
    <!-- Header: mx-auto + w-full for centering -->
    <header class="w-full bg-blue-100 border border-black p-1">
      <h1 class="text-md text-center font-bold">
        Bespoke Pharmacist-led medication reviews
      </h1>
      <div class="w-full border border-black p-1 bg-black">
        <p class="text-center text-md font-semibold text-slate-200">
          Licensed in Wisconsin
        </p>
      </div>
    </header>

    <div
      class="relative w-full min-h-[800px] flex items-center justify-center overflow-hidden font-sans p-4"
    >
      <!-- 1. Background Layer: Full opacity but we will use an overlay -->
      <div
        class="absolute inset-0 bg-cover bg-center bg-no-repeat"
        :style="{ backgroundImage: `url(${heroImageUrl})` }"
      ></div>

      <!-- 2. Dark Overlay: This helps the white "card" pop -->
      <div class="absolute inset-0 bg-black/30"></div>

      <!-- 3. The Content Card: Glassmorphism effect -->
      <!-- bg-white/80 adds transparency, backdrop-blur makes the background image non-distracting -->
      <div
        class="relative z-10 max-w-2xl w-full bg-white/60 backdrop-blur-md p-8 md:p-12 rounded-3xl shadow-2xl text-center border border-black"
      >
        <!-- Tagline -->
        <span
          class="inline-block py-1.5 px-4 mb-6 text-xs font-bold tracking-widest text-blue-700 uppercase bg-blue-50 rounded-full border border-blue-100"
        >
          Personalized Care
        </span>

        <!-- Main Headline: Balanced contrast -->
        <h1
          class="text-4xl md:text-5xl font-extrabold text-slate-900 tracking-tight leading-[1.1]"
        >
          One-to-One Extensive <br />
          <span class="text-blue-600">medication reviews</span>
        </h1>

        <!-- Description: High contrast slate color -->
        <p
          class="mt-6 text-lg md:text-xl text-black font-medium leading-relaxed"
        >
          Get personalized advice and recommendations directly from
          professionals.
        </p>

        <!-- WebMD line: Subtle but distinct -->
        <p class="mt-4 text-md text-red-600 font-semibold">
          Stop stressing over WebMD searches
        </p>

        <!-- Button: Solid color for maximum visibility -->
        <div class="mt-10">
          <button
            class="w-full md:w-auto px-12 py-4 bg-blue-600 hover:bg-blue-700 text-white font-bold text-lg rounded-xl transition-all shadow-lg hover:shadow-blue-200"
          >
            Learn more
          </button>
        </div>
      </div>
    </div>
    <!-- Main Content Container -->
    <div
      ref="targetElement"
      :class="[
        'w-full transition-all duration-3000 transform flex flex-col items-center',
        isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10',
      ]"
    >
      <!-- Main "Chat" Container -->
      <main
        class="w-full p-4 flex flex-col gap-6 bg-gradient-to-tr from-slate-950 via-indigo-950 to-slate-900 rounded-b-3xl shadow-2xl relative border-b border-white/10 overflow-hidden"
      >
        <!-- Geometric Pattern Overlay -->
        <div
          class="absolute inset-0 pointer-events-none opacity-[0.05]"
          style="
            background-color: #e5e5f7;
            background-image:
              repeating-linear-gradient(
                45deg,
                #81829d 25%,
                transparent 25%,
                transparent 75%,
                #81829d 75%,
                #81829d
              ),
              repeating-linear-gradient(
                45deg,
                #81829d 25%,
                #e5e5f7 25%,
                #e5e5f7 75%,
                #81829d 75%,
                #81829d
              );
            background-position:
              0 0,
              4px 4px;
            background-size: 8px 8px;
          "
        ></div>
        <p class="text-center text-white font-semibold text-xl">
          Got questions? We've got answers!
        </p>
        <!-- Message 1 (Left/Pharmacist) -->
        <div class="w-[85%] self-start flex flex-col gap-1">
          <div
            class="bg-white rounded-2xl rounded-tl-none p-5 shadow-lg border-l-4 border-blue-500"
          >
            <p class="text-slate-900 font-bold text-lg mb-2">
              What do we offer?
            </p>
            <p class="text-slate-600 leading-relaxed">
              A simple way to get answers for all your medication related
              concerns!
            </p>
          </div>
        </div>

        <!-- Message 2 (Right/User perspective) -->
        <div class="w-[85%] self-end flex flex-col gap-1 relative">
          <div
            class="bg-blue-600 rounded-2xl rounded-tr-none p-5 shadow-xl text-white border-r-4 border-white"
          >
            <p class="font-bold text-lg mb-2">
              What kind of questions can you answer?
            </p>
            <p class="text-blue-50 leading-relaxed">
              We are focused on answering every concern you may have, providing
              a bespoke personalized medication and life-style review.
            </p>
          </div>

          <!-- FADE OVERLAY: Only shows when NOT expanded -->
          <div
            v-if="!isExpanded"
            class="absolute inset-x-0 bottom-0 h-24 bg-gradient-to-t from-slate-900 to-transparent pointer-events-none"
          ></div>
        </div>

        <!-- COLLAPSIBLE SECTION -->
        <div
          class="flex flex-col gap-4 overflow-hidden transition-all duration-700 ease-in-out"
          :style="{
            maxHeight: isExpanded ? '1000px' : '0px',
            opacity: isExpanded ? '1' : '0',
          }"
        >
          <!-- Message 3 (Left) -->
          <div class="w-[85%] self-start flex flex-col gap-1">
            <div
              class="bg-white rounded-2xl rounded-tl-none p-5 shadow-lg border-l-4 border-blue-500"
            >
              <p class="text-slate-900 font-bold text-lg mb-2 text-left">
                What is the benefit? I already see a doctor.
              </p>
              <p class="text-slate-600 text-left leading-relaxed">
                We do not work to KPI Targets to line the pockets of a rich CEO.
                We take as much time as needed to fully review every element of
                your health report.
              </p>
            </div>
          </div>

          <!-- Message 4 (Right) -->
          <div class="w-[85%] self-end flex flex-col gap-1">
            <div
              class="bg-blue-600 rounded-2xl rounded-tr-none p-5 shadow-xl text-white border-r-4 border-white"
            >
              <p class="font-bold text-lg mb-2 text-right">
                What kind of questions can you answer?
              </p>
              <p class="text-blue-50 text-right leading-relaxed">
                We are focused on answering every concern you may have,
                providing a bespoke personalized medication and life-style
                review.
              </p>
            </div>
          </div>
        </div>

        <!-- VIEW MORE BUTTON -->
        <div class="flex justify-center mt-4">
          <button
            @click="isExpanded = !isExpanded"
            class="group flex items-center gap-2 px-6 py-2 bg-slate-800 hover:bg-slate-700 text-blue-400 font-bold rounded-full border border-slate-700 transition-all shadow-md"
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
    <!-- Section Wrapper -->
    <div class="w-full bg-slate-50 py-8 px-4 flex flex-col items-center">
      <!-- Section Title -->
      <div class="max-w-2xl w-full mb-12">
        <h2
          class="text-center text-2xl md:text-3xl font-extrabold text-slate-900 leading-tight"
        >
          Getting the knowledge you want <br />
          <span class="text-blue-600">has never been easier</span>
        </h2>
        <div class="h-1 w-20 bg-blue-600 mx-auto mt-4 rounded-full"></div>
      </div>

      <!-- Steps Container -->
      <div class="max-w-2xl w-full space-y-6 md:space-y-12 relative">
        <!-- Vertical Line (The timeline connector) -->
        <div
          class="absolute left-6 top-0 bottom-0 w-0.5 bg-slate-200 z-0"
        ></div>

        <!-- Step One -->
        <div class="relative z-10 flex gap-6 group">
          <div
            class="flex-shrink-0 w-12 h-12 rounded-full bg-white border-2 border-blue-600 flex items-center justify-center font-bold text-blue-600 shadow-sm group-hover:bg-blue-600 group-hover:text-white transition-colors"
          >
            1
          </div>
          <div
            class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100 flex-1"
          >
            <h3
              class="text-sm font-bold uppercase tracking-widest text-slate-400 mb-2"
            >
              The Problem
            </h3>
            <p class="text-slate-700 leading-relaxed">
              Regular doctors and pharmacists do all they can to help, but they
              are often limited by corporate targets, putting efficiency above
              all else.
              <span class="block mt-2 font-semibold text-blue-700 italic">
                "This often leads to people being treated like numbers on a
                conveyor belt."
              </span>
            </p>
          </div>
        </div>

        <!-- Step Two -->
        <div class="relative z-10 flex gap-6 group">
          <div
            class="flex-shrink-0 w-12 h-12 rounded-full bg-white border-2 border-blue-600 flex items-center justify-center font-bold text-blue-600 shadow-sm group-hover:bg-blue-600 group-hover:text-white transition-colors"
          >
            2
          </div>
          <div
            class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100 flex-1"
          >
            <h3
              class="text-sm font-bold uppercase tracking-widest text-slate-400 mb-2"
            >
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

        <!-- Step Three -->
        <div class="relative z-10 flex gap-6 group">
          <div
            class="flex-shrink-0 w-12 h-12 rounded-full bg-white border-2 border-blue-600 flex items-center justify-center font-bold text-blue-600 shadow-sm group-hover:bg-blue-600 group-hover:text-white transition-colors"
          >
            3
          </div>
          <div
            class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100 flex-1"
          >
            <h3
              class="text-sm font-bold uppercase tracking-widest text-slate-400 mb-2"
            >
              The Action Plan
            </h3>
            <p class="text-slate-700 leading-relaxed">
              We focus on reducing waste, managing side effects, and creating a
              <span class="text-indigo-600 font-bold"
                >Personalized Medication Action Plan</span
              >
              designed specifically for your lifestyle and health goals.
            </p>
          </div>
        </div>
      </div>

      <!-- Bottom CTA/Success Message -->
      <div class="mt-4 max-w-xl w-full">
        <div
          class="bg-gradient-to-r from-blue-600 to-indigo-700 p-8 rounded-3xl shadow-xl text-center transform hover:scale-[1.02] transition-transform"
        >
          <p class="text-white text-2xl font-bold">
            Click here to
            <span class="text-slate-900 text-3xl">Get Started.</span>
          </p>
        </div>
      </div>
    </div>
    <div>
      <div class="min-h-screen bg-slate-300">
        <!-- Enquiry Form Section -->
        <div
          id="enquiry-form"
          class="w-full bg-slate-800 py-8 px-2 flex flex-col items-center"
        >
          <div
            class="max-w-3xl w-full bg-white rounded-[2.5rem] shadow-2xl overflow-hidden border border-white/20"
          >
            <!-- Form Header -->
            <div
              class="bg-gradient-to-r from-blue-600 to-indigo-700 p-8 text-center"
            >
              <h2 class="text-3xl font-extrabold text-white">
                Start Your Review
              </h2>
              <p class="text-blue-100 mt-2 font-medium">
                Fill out the form below and a pharmacist will reach out to you
                shortly.
              </p>
            </div>

            <!-- Form Body -->
            <form
              @submit.prevent="handleFormSubmit"
              class="p-8 md:p-12 space-y-6"
            >
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Name -->
                <div class="flex flex-col gap-2">
                  <label
                    for="name"
                    class="text-sm font-bold text-slate-700 uppercase tracking-wider"
                    >Full Name</label
                  >
                  <input
                    v-model="form.name"
                    type="text"
                    id="name"
                    required
                    placeholder="John Doe"
                    class="px-4 py-3 rounded-xl border border-slate-200 focus:ring-2 focus:ring-blue-600 focus:border-transparent outline-none transition-all text-slate-900"
                  />
                </div>

                <!-- Email -->
                <div class="flex flex-col gap-2">
                  <label
                    for="email"
                    class="text-sm font-bold text-slate-700 uppercase tracking-wider"
                    >Email Address</label
                  >
                  <input
                    v-model="form.email"
                    type="email"
                    id="email"
                    required
                    placeholder="john@example.com"
                    class="px-4 py-3 rounded-xl border border-slate-200 focus:ring-2 focus:ring-blue-600 focus:border-transparent outline-none transition-all text-slate-900"
                  />
                </div>
              </div>

              <!-- Phone (Optional) -->
              <div class="flex flex-col gap-2">
                <label
                  for="phone"
                  class="text-sm font-bold text-slate-700 uppercase tracking-wider"
                  >Phone Number (Optional)</label
                >
                <input
                  v-model="form.phone"
                  type="tel"
                  id="phone"
                  placeholder="(555) 000-0000"
                  class="px-4 py-3 rounded-xl border border-slate-200 focus:ring-2 focus:ring-blue-600 focus:border-transparent outline-none transition-all text-slate-900"
                />
              </div>

              <!-- Message -->
              <div class="flex flex-col gap-2">
                <label
                  for="message"
                  class="text-sm font-bold text-slate-700 uppercase tracking-wider"
                  >How can we help?</label
                >
                <textarea
                  v-model="form.message"
                  id="message"
                  rows="4"
                  required
                  placeholder="Tell us a bit about your current medications or concerns..."
                  class="px-4 py-3 rounded-xl border border-slate-200 focus:ring-2 focus:ring-blue-600 focus:border-transparent outline-none transition-all text-slate-900"
                ></textarea>
              </div>

              <!-- Submit Button -->
              <div class="pt-4">
                <button
                  type="submit"
                  class="w-full py-4 bg-blue-600 hover:bg-blue-700 text-white font-bold text-lg rounded-xl transition-all shadow-lg hover:shadow-blue-200 flex items-center justify-center gap-2"
                >
                  <span>Submit Enquiry</span>
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    class="h-5 w-5"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z"
                      clip-rule="evenodd"
                    />
                  </svg>
                </button>
              </div>

              <!-- Privacy Note -->
              <p class="text-center text-xs text-slate-400">
                Your information is kept confidential and is only used to
                contact you regarding your review.
              </p>
            </form>
          </div>

          <!-- Footer Brand -->
          <footer class="mt-12 text-slate-500 text-sm">
            &copy; {{ new Date().getFullYear() }} Pharmacist-Led Medication
            Reviews. Licensed in Wisconsin.
          </footer>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// 1. Import the image so Vite can process it and provide the correct URL
import heroImageUrl from "@/assets/backgroundHero.jpg";
import { ref, onMounted, onUnmounted, reactive } from "vue";
const targetElement = ref(null);
const isVisible = ref(false);
const isExpanded = ref(false);

// Logic for the observer
let observer = null;

const form = reactive({
  name: "",
  email: "",
  phone: "",
  message: "",
});
const handleFormSubmit = () => {
  // Replace this with your actual submission logic (e.g., API call)
  console.log("Form Submitted:", form);
  alert("Thank you! Your enquiry has been sent. We will contact you soon.");

  // Reset form
  form.name = "";
  form.email = "";
  form.phone = "";
  form.message = "";
};

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

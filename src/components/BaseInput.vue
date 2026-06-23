<template>
  <div class="flex flex-col gap-2">
    <!-- Main Group Label -->
    <label v-if="label" class="text-sm font-bold text-slate-700 uppercase">
      {{ label }}
    </label>

    <!-- RADIO LAYOUT -->
    <div v-if="type === 'radio'" class="flex gap-6 mt-1">
      <label
        v-for="option in options"
        :key="option.value"
        class="flex items-center gap-2 cursor-pointer group"
      >
        <div class="relative flex items-center justify-center">
          <input
            type="radio"
            :name="label"
            :value="option.value"
            :checked="modelValue === option.value"
            @change="$emit('update:modelValue', option.value)"
            v-bind="$attrs"
            class="peer appearance-none w-5 h-5 border-2 border-black rounded-full checked:border-blue-600 transition-all cursor-pointer"
          />
          <!-- Custom Inner Circle -->
          <div
            class="absolute w-2.5 h-2.5 rounded-full bg-blue-600 scale-0 peer-checked:scale-100 transition-transform"
          ></div>
        </div>
        <span
          class="text-slate-800 font-medium group-hover:text-blue-600 transition-colors"
        >
          {{ option.label }}
        </span>
      </label>
    </div>

    <!-- TEXTAREA (Existing) -->
    <textarea
      v-else-if="type === 'textarea'"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      v-bind="$attrs"
      class="px-4 py-3 rounded-xl border-2 border-black focus:ring-2 focus:ring-blue-600 focus:border-transparent outline-none transition-all text-slate-900"
    ></textarea>

    <!-- STANDARD INPUT (Existing) -->
    <input
      v-else
      :type="type"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      v-bind="$attrs"
      class="px-4 py-3 rounded-xl border-2 border-black focus:ring-2 focus:ring-blue-600 focus:border-transparent outline-none transition-all text-slate-900"
    />
  </div>
</template>

<script setup>
defineProps({
  label: String,
  modelValue: [String, Number, Boolean],
  type: {
    type: String,
    default: "text",
  },
  options: {
    type: Array,
    default: () => [],
  },
});
defineEmits(["update:modelValue"]);
</script>

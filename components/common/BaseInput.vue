<template>
  <div>
    <label
      v-if="label"
      :class="[labelClass, 'fw-semibold', 'fs-8', 'mb-1', 'd-block' , 'base_color']"
      >{{ label }}</label
    >
    <div class="position-relative">
      <input
        :class="[
          showEye && 'pe-5',
          'form-control',
          'base_input',
          error && 'is-invalid',
        ]"
        :type="showPassword ? 'text' : type"
        :placeholder="placeholder"
        v-bind="$attrs"
        @input="$emit('update:modelValue', $event.target.value)"
        :value="modelValue"
      />
      <Eye
        v-if="showEye"
        @click="showPassword = !showPassword"
        class="position-absolute eye_icon"
        :style="{ 'right': error ? '32px' : '16px' }"
      />
    </div>
    <div v-if="error" class="error mt-1 fs-7">{{ error }}</div>
  </div>
</template>

<script setup>
import Eye from "../icons/Eye.vue";
import { ref } from "vue";
const showPassword = ref(false);

defineProps({
  label: {
    type: String,
    default: "",
  },
  labelClass: {
    type: String,
    default: "",
  },
  placeholder: {
    type: String,
    default: "placeholder",
  },
  type: {
    type: String,
    default: "text",
  },
  showEye: {
    type: Boolean,
    default: false,
  },
  modelValue: {
    type: String,
    default: "",
  },
  error: {
    type: [String, Boolean],
    default: "",
  },
});
</script>

<template>
  <button :type="type" :disabled="disabled" class="btn custom_btn">
    <slot v-if="!loading"></slot>
    <Loader v-else />
  </button>
</template>

<script setup>
import Loader from "./Loader.vue";

defineProps({
  // Define props for dynamic attributes
  type: {
    type: String,
    default: "button",
  },
  disabled: {
    type: Boolean,
    default: false,
  },
  loading: {
    type: Boolean,
    default: false,
  },
  // You can add more props for other attributes as needed
});
</script>

<template>
  <div class="signIn_container">
    <div class="row">
      <div class="col-12 mb-5">
        <BidIngine />
      </div>
      <div class="col-12 fw-semibold fs-4 mb-4 base_color">
        Sign in to Bid Engine
      </div>
      <div class="col-12 mb-3">
        <BaseInput
          type="text"
          label="Email Address"
          placeholder="Enter Email Address"
          v-model="email"
          :error="btnTouched && emailError"
        />
      </div>
      <div class="col-12">
        <div class="d-flex justify-content-between align-items-center mb-1">
          <label class="fs-8 fw-semibold base_color">Password</label>
          <a class="fs-7" href="#">Forgotten your password?</a>
        </div>
        <BaseInput
          showEye
          type="password"
          placeholder="Start typing ..."
          v-model="password"
          :error="btnTouched && passwordError"
        />
      </div>
      <div class="col-12 mt-4">
        <Button
          :loading="loading"
          :disabled="btnDisabled || loading"
          class="col-12"
          @click="submitForm"
          >Sign in</Button
        >
      </div>
      <div class="col-12 mt-3 text-center">
        <span class="fs-7 color_blind"
          >Don’t have an account? <a href="/signup/"> Sign up</a></span
        >
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
import { useForm, useField } from "vee-validate";
import { signInSchema } from "../schema";
import BaseInput from "./common/BaseInput.vue";
import BidIngine from "./icons/BidIngine.vue";
import Button from "./common/Button.vue";

const btnTouched = ref(false);
const loading = ref(false);
const { validate, resetForm } = useForm({
  validationSchema: signInSchema,
});

const { value: email, errorMessage: emailError } = useField("email");
const { value: password, errorMessage: passwordError } = useField("password");

const btnDisabled = computed(() => {
  return  !email.value || !password.value
})

const submitForm = async () => {
  btnTouched.value = true;
  const { valid } = await validate(); // Trigger validation
  if (valid) {
    loading.value = true;
    console.log("data:", "email:", email.value, "password:", password.value);
    setTimeout(() => {
      resetForm();
      loading.value = false;
    }, 2000);
  } else {
    console.log("Form is invalid. Cannot submit.");
  }
};
</script>

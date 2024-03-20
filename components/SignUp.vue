<template>
  <div class="signIn_container py-5 py-sm-3">
    <div class="row">
      <div class="col-12 mb-5">
        <BidIngine />
      </div>
      <div class="col-12 fw-semibold fs-4 mb-4 base_color">
        Sign up to Bid Engine
      </div>
      <div class="col-12">
        <div class="row">
          <div class="col-6 mb-3 pr_adjust">
            <BaseInput
              v-model="firstName"
              :error="btnTouched && firstNameError"
              placeholder="First Name"
              label="First Name"
            />
          </div>
          <div class="col-6 mb-3 pl_adjust">
            <BaseInput
              v-model="lastName"
              :error="btnTouched && lastNameError"
              placeholder="Last Name"
              label="Last Name"
            />
          </div>
          <div class="col-sm-6 mb-3">
            <BaseInput
              type="email"
              placeholder="Email Address"
              label="Email Address"
              v-model="email"
              :error="btnTouched && emailError"
            />
          </div>
          <div class="col-sm-6 mb-3">
            <BaseInput
              type="number"
              placeholder="(123) 456 78 90"
              label="Phone Number"
              v-model="phoneNumber"
              :error="btnTouched && phoneError"
            />
          </div>
          <div class="col-sm-6 mb-3">
            <BaseInput
              v-model="companyName"
              :error="btnTouched && companyNameError"
              placeholder="Company Name"
              label="Company Name"
            />
          </div>
          <div class="col-sm-6 mb-3">
            <BaseInput
              v-model="companyWebsite"
              :error="btnTouched && companyWebsiteError"
              placeholder="Company Website"
              label="Company Website"
            />
          </div>
          <div class="col-6 mb-3 pr_adjust">
            <BaseInput
              showEye
              v-model="password"
              :error="btnTouched && passwordError"
              placeholder="Start typing ..."
              type="password"
              label="Password"
            />
          </div>
          <div class="col-6 mb-3 pl_adjust">
            <BaseInput
              v-model="confirmPassword"
              :error="btnTouched && confirmPasswordError"
              type="password"
              placeholder="Start typing ..."
              label="Confirm Password"
              showEye
            />
          </div>

          <div class="col-12 mt-3">
            <Button
              :loading="loading"
              :disabled="btnDisabled || loading"
              class="col-12"
              @click="submitForm"
              >Create Account</Button
            >
          </div>
          <div class="col-12 mt-3 text-center">
            <span class="fs-7 color_blind"
              >Already have an account? <a href="/sign-in/"> Sign in</a></span
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useForm, useField } from "vee-validate";
import BaseInput from "./common/BaseInput.vue";
import BidIngine from "./icons/BidIngine.vue";
import Button from "./common/Button.vue";
import { computed, ref } from "vue";
import { signUpSchema } from "../schema";

const btnTouched = ref(false);
const loading = ref(false);
const { validate, resetForm } = useForm({
  validationSchema: signUpSchema,
});

const { value: firstName, errorMessage: firstNameError } =
  useField("firstName");
const { value: lastName, errorMessage: lastNameError } = useField("lastName");
const { value: email, errorMessage: emailError } = useField("email");
const { value: phoneNumber, errorMessage: phoneError } =
  useField("phoneNumber");
const { value: companyName, errorMessage: companyNameError } =
  useField("companyName");
const { value: companyWebsite, errorMessage: companyWebsiteError } =
  useField("companyWebsite");
const { value: password, errorMessage: passwordError } = useField("password");
const { value: confirmPassword, errorMessage: confirmPasswordError } =
  useField("confirmPassword");

const btnDisabled = computed(() => {
  return (
    !firstName.value ||
    !lastName.value ||
    !email.value ||
    !phoneNumber.value ||
    !companyName.value ||
    !companyWebsite.value ||
    !password.value ||
    !confirmPassword.value
  );
});
const submitForm = async () => {
  btnTouched.value = true;
  const { valid } = await validate(); // Trigger validation
  if (valid) {
    loading.value = true;
    const data = {
      firstName: firstName.value,
      lastName: lastName.value,
      email: email.value,
      phoneNumber: phoneNumber.value,
      companyName: companyName.value,
      companyWebsite: companyWebsite.value,
      password: password.value,
      confirmPassword: confirmPassword.value,
    };
    console.log(data);
    setTimeout(() => {
      resetForm();
      loading.value = false;
    }, 2000);
  } else {
    console.log("Form is invalid. Cannot submit.");
  }
};
</script>

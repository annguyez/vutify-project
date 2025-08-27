<template>
  <v-form ref="formRef" v-model="isValid" lazy-validation>
    <div class="text-h5 mb-6 text-left">Login</div>

    <!-- Phone -->
    <v-text-field
      v-model="phone"
      label="Enter phone number"
      type="tel"
      prepend-inner-icon="mdi-phone"
      clearable
      variant="outlined"
      density="comfortable"
      :rules="phoneRules"
    />

    <!-- Captcha -->
    <v-text-field
      v-model="captcha"
      label="Enter captcha below"
      prepend-inner-icon="mdi-shield-lock-outline"
      variant="outlined"
      density="comfortable"
      :rules="captchaRules"
    >
      <template #append-inner>
        <v-btn icon="mdi-refresh" variant="text" @click="refreshCaptcha" />
      </template>
    </v-text-field>

    <!-- Captcha Image -->
    <div class="d-flex justify-center my-3">
      <v-img
        src="https://dummyimage.com/250x60/cccccc/000000&text=YSD6MV"
        height="60"
        width="250"
        class="rounded"
      />
    </div>

    <!-- Login button -->
    <v-btn block color="primary" size="large" class="mt-4" @click="submit">
      Log in
    </v-btn>
  </v-form>
</template>

<script setup>
import { ref } from 'vue'

const phone = ref('')
const captcha = ref('')
const isValid = ref(false)
const formRef = ref(null)

const phoneRules = [
  v => !!v || 'Phone number is required',
  v => /^0\d{9}$/.test(v) || 'Phone must be 10 digits and start with 0',
]

const captchaRules = [
  v => !!v || 'Captcha is required',
  v => v.length >= 4 || 'Captcha must be at least 4 characters',
]

const refreshCaptcha = () => {
  console.log('Refresh captcha')
}

const submit = async () => {
  const result = await formRef.value?.validate()
  if (result.valid) {
    alert(`Login success!\nPhone: ${phone.value}\nCaptcha: ${captcha.value}`)
  }
}
</script>

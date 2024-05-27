<template>
  <div class="h-screen flex items-center justify-center">
    <div v-if="!success" class="h-3/4 flex gap-4 items-center bg-white rounded-2xl p-8">
      <div class="w-[360px] pl-4">
        <h2 class="text-4xl font-bold text-slate-800">Stay updated!</h2>
        <p class="text-sm mt-4 text-slate-800">
          Join 60,000+ product managers receiving monthly updates on:
        </p>

        <ul class="text-slate-700 mt-6 space-y-2">
          <li class="flex items-center text-sm gap-4">
            <img src="./assets/images/icon-list.svg" alt="icon-list" />
            <span>Product discovery and building what matters</span>
          </li>
          <li class="flex items-center text-sm gap-4">
            <img src="./assets/images/icon-list.svg" alt="icon-list" />
            <span>Measuring to ensure updates are a success</span>
          </li>
          <li class="flex items-center text-sm gap-4">
            <img src="./assets/images/icon-list.svg" alt="icon-list" />
            <span>And much more!</span>
          </li>
        </ul>

        <form action="" class="mt-8" @submit.prevent="handleSubmit">
          <div class="flex flex-col gap-1">
            <div class="flex items-center justify-between">
              <label for="email" class="text-sm font-bold text-slate-800">Email address</label>
              <span v-if="error" class="text-xs font-semibold text-[#ff6257]"
                >Valid email required!</span
              >
            </div>
            <input
              type="email"
              class="border-2 p-2 px-4 rounded-lg"
              v-model="email"
              @keyup.prevent="isValidEmail"
              :class="hasError()"
              placeholder="email@company.com"
            />
          </div>

          <button
            type="submit"
            class="w-full mt-4 py-4 text-center rounded-lg text-sm font-semibold text-white bg-slate-900 hover:bg-[#ff6257] hover:drop-shadow-md"
          >
            Subscribe to monthly newsletter
          </button>
        </form>
      </div>
      <div
        class="w-[320px] rounded-2xl h-full"
        style="
          background-image: url('./illustration-sign-up-desktop.svg');
          background-position: center;
          background-size: cover;
        "
      >
        &nbsp;
      </div>
    </div>
    <div v-else class="bg-white rounded-2xl w-[380px] p-8 space-y-6">
      <div class="w-12">
        <img src="./assets/images/icon-success.svg" alt="Success" />
      </div>
      <h2 class="text-slate-900 font-bold text-3xl mt-4">Thanks for subscribing!</h2>

      <p class="text-sm mt-4 leading-6 text-slate-800">
        A confirmation email has been sent to <strong>{{ email }}.</strong> Please open it and click
        <br />the button inside to confirm your subscription
      </p>
      <button
        type="button"
        @click.prevent="dismiss"
        class="w-full mt-4 py-4 text-center rounded-lg text-sm font-semibold text-white bg-slate-900 hover:bg-[#ff6257] hover:drop-shadow-md"
      >
        Dismiss message
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const error = ref(false)
const success = ref(false)
const email = ref('')

const hasError = () => {
  return error.value ? 'bg-red-100 border-[#ff6257] text-[#ff6257]' : 'border-slate-800'
}

const isValidEmail = () => {
  setTimeout(() => {
    if (!/^[^@]+@\w+(\.\w+)+\w$/.test(email.value)) {
      error.value = true
    } else {
      error.value = false
    }
  }, 1000)
}

const handleSubmit = () => {
  if (error.value === false && email.value) {
    success.value = true
  }else {
    error.value = true
  }
}

const dismiss = () => {
  success.value = false
  email.value = ''
}
</script>

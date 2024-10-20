<template>
  <div class="">
    <div class="h-full">
      <backdrop />
    </div>
    <header class="max-w-7xl mx-auto flex items-center justify-between px-4">
      <img class="h-16 sm:h-24"
        src="https://images.squarespace-cdn.com/content/v1/556535dbe4b0f94763ababe6/1585758017258-IA6ETGNHS8NZUVAV1SBW/logo-3.gif?format=1500w"
        alt="">
      <div class="flex items-center gap-2 flex-row-reverse">
        <button
          class="hidden  rounded-full p-1 text-center text-xs font-semibold leading-5 ring-1 ring-inset ring-gray-200 hover:ring-0 bg-[#8F0403] text-white px-6 py-2 sm:flex items-center gap-3 hover:scale-95 transition-all duration-300 hover:shadow-lg hover:shadow-[#8F0403]">Signup
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="size-5">
            <path fill-rule="evenodd"
              d="M2 10a.75.75 0 0 1 .75-.75h12.59l-2.1-1.95a.75.75 0 1 1 1.02-1.1l3.5 3.25a.75.75 0 0 1 0 1.1l-3.5 3.25a.75.75 0 1 1-1.02-1.1l2.1-1.95H2.75A.75.75 0 0 1 2 10Z"
              clip-rule="evenodd" />
          </svg>
        </button>
        <button @click="toggleDarkMode" class="p-2">
          <span v-if="isDarkMode" class="text-white flex items-center gap-2  border px-4 py-1 rounded-full w-full">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="size-5">
              <path
                d="M10 2a.75.75 0 0 1 .75.75v1.5a.75.75 0 0 1-1.5 0v-1.5A.75.75 0 0 1 10 2ZM10 15a.75.75 0 0 1 .75.75v1.5a.75.75 0 0 1-1.5 0v-1.5A.75.75 0 0 1 10 15ZM10 7a3 3 0 1 0 0 6 3 3 0 0 0 0-6ZM15.657 5.404a.75.75 0 1 0-1.06-1.06l-1.061 1.06a.75.75 0 0 0 1.06 1.06l1.06-1.06ZM6.464 14.596a.75.75 0 1 0-1.06-1.06l-1.06 1.06a.75.75 0 0 0 1.06 1.06l1.06-1.06ZM18 10a.75.75 0 0 1-.75.75h-1.5a.75.75 0 0 1 0-1.5h1.5A.75.75 0 0 1 18 10ZM5 10a.75.75 0 0 1-.75.75h-1.5a.75.75 0 0 1 0-1.5h1.5A.75.75 0 0 1 5 10ZM14.596 15.657a.75.75 0 0 0 1.06-1.06l-1.06-1.061a.75.75 0 1 0-1.06 1.06l1.06 1.06ZM5.404 6.464a.75.75 0 0 0 1.06-1.06l-1.06-1.06a.75.75 0 1 0-1.061 1.06l1.06 1.06Z" />
            </svg>
            <span class="text-xs">Light mode</span>
          </span>
          <span class="flex items-center gap-2 border px-4 py-1 rounded-full w-full" v-else>
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="size-5">
              <path fill-rule="evenodd"
                d="M7.455 2.004a.75.75 0 0 1 .26.77 7 7 0 0 0 9.958 7.967.75.75 0 0 1 1.067.853A8.5 8.5 0 1 1 6.647 1.921a.75.75 0 0 1 .808.083Z"
                clip-rule="evenodd" />
            </svg>
            <span class="text-xs">Dark mode</span>
          </span>
        </button>
      </div>
    </header>
    <main class="flex min-h-screen overflow-hidden pt-16 sm:py-28">
      <div class="mx-auto flex w-full max-w-5xl flex-col px-2 sm:px-6">
        <div
          class="-m-2 grid grid-cols-1 rounded-3xl shadow-[inset_0_0_2px_1px_#ffffff4d] ring-1 ring-black/5 max-w-xl mx-auto w-full lg:max-w-full">
          <div class="grid grid-cols-1 rounded-4xl p-2 shadow-md shadow-black/5">
            <div class="rounded-3xl dark:bg-black bg-white shadow-2xl ring-1 ring-black/5 grid lg:grid-cols-2">
              <div class="py-10 p-4 sm:p-10">
                <div class="flex justify-start">
                  <fieldset aria-label="Payment frequency">
                    <RadioGroup v-model="frequency"
                      class="grid grid-cols-2 gap-x-1 rounded-full p-1 text-center text-xs font-semibold leading-5 ring-1 ring-inset dark:ring-gray-700 ring-gray-200">
                      <RadioGroupOption as="template" v-for="option in frequencies" :key="option.value" :value="option"
                        v-slot="{ checked }">
                        <div
                          :class="[checked ? 'bg-[#8F0403] text-white' : 'dark:text-gray-300 text-gray-500', 'cursor-pointer rounded-full px-5 py-1']">
                          {{ option.label }}</div>
                      </RadioGroupOption>
                    </RadioGroup>
                  </fieldset>
                </div>
                <h1 class="dark:text-white text-gray-950 font-semibold text-xl py-5">Signin as a <span>{{
                  frequency.value === 'monthly' ? 'Student' : 'Admin' }}</span></h1>
                <form @submit.prevent="handleSubmit" class="h-full flex flex-col justify-start">
                  <div class="space-y-6">
                    <div>
                      <label for="email" class="mb-2 block text-sm font-medium dark:text-white text-gray-700">Email
                        address</label>
                      <input id="email" v-model="email" @blur="validateEmail" autocomplete="email" required=""
                        class="block w-full appearance-none rounded-lg border dark:border-gray-700 border-gray-200 dark:bg-black bg-white py-[calc(theme(spacing.2)-1px)] px-[calc(theme(spacing.3)-1px)] dark:text-gray-50 text-gray-900 placeholder:text-gray-400 focus:border-[#8F0403] focus:outline-none focus:ring-cyan-500 sm:text-sm"
                        type="email" />
                      <p v-if="emailError" class="text-red-500 text-sm">{{ emailError }}</p>
                    </div>
                    <div>
                      <div class="relative">
                        <label for="password"
                          class="mb-2 block text-sm font-medium dark:text-white text-gray-700">Password</label>
                        <input :type="isPasswordVisible ? 'text' : 'password'" id="password" v-model="password"
                          @blur="validatePassword" autocomplete="current-password" required
                          class="block w-full appearance-none rounded-lg border dark:border-gray-700 border-gray-200 dark:bg-black/90 bg-white py-[calc(theme(spacing.2)-1px)] px-[calc(theme(spacing.3)-1px)] dark:text-gray-50 text-gray-900 placeholder:text-gray-400 focus:border-[#8F0403] focus:outline-none focus:ring-cyan-500 sm:text-sm" />
                        <span class="absolute right-2 top-9 cursor-pointer dark:text-gray-300 text-gray-500"
                          @click="togglePasswordVisibility">
                          <Eye v-if="isPasswordVisible" />
                          <crossEye v-else />
                        </span>
                      </div>
                      <p v-if="passwordError" class="text-red-500 text-sm">{{ passwordError }}</p>
                    </div>
                  </div>
                  <button
                    class="inline-flex justify-center rounded-lg py-2 px-3 text-sm font-semibold outline-2 outline-offset-2 relative overflow-hidden bg-[#8F0403] text-white before:absolute before:inset-0 active:before:bg-transparent hover:before:bg-white/10 active:bg-[#8F0403]/10 active:text-white/80 before:transition-colors mt-8 w-full hover:scale-95 transition-all duration-300 hover:shadow-md hover:shadow-[#8F0403]"
                    type="submit">
                    Sign in to account
                  </button>
                  <p v-if="loginError" class="text-red-500 text-sm mt-4">{{ loginError }}</p>
                  <div class="border-t border-gray-200 mt-10 flex items-center justify-between gap-3 pt-10">
                    <div
                      class="border dark:border-gray-700 w-full rounded p-2 flex items-center gap-2 justify-center cursor-pointer hover:dark:bg-gray-950 hover:bg-gray-50 hover:scale-90 transition-all duration-300">
                      <facebook />
                      <span class="text-xs text-gray-400">Facebook</span>
                    </div>
                    <div
                      class="border dark:border-gray-700 w-full rounded p-2 flex items-center gap-2 justify-center cursor-pointer hover:dark:bg-gray-950 hover:bg-gray-50 hover:scale-90 transition-all duration-300">
                     <google />
                      <span class="text-xs text-gray-400">Google</span>
                    </div>
                    <div
                      class="border dark:border-gray-700 w-full rounded p-2 flex items-center gap-2 justify-center cursor-pointer hover:dark:bg-gray-950 hover:bg-gray-50 hover:scale-90 transition-all duration-300">
                     <mail />
                      <span class="text-xs text-gray-400">Email</span>
                    </div>
                  </div>
                </form>
              </div>
              <div
                class="hidden relative lg:flex aspect-square flex-col justify-end overflow-hidden rounded-r-3xl sm:aspect-[3/4] lg:aspect-[3/4]">
                <img alt="" src="https://plus.unsplash.com/premium_photo-1673371666142-91643e6b03af?q=80&w=3387&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
                  class="absolute inset-0 object-cover">
                <div aria-hidden="true"
                  class="absolute inset-0 rounded-r-3xl bg-gradient-to-t from-black from-10% to-75% ring-1 ring-inset ring-gray-950/10 lg:from-25%">
                </div>
                <figure class="relative p-10">
                  <blockquote>
                    <p
                      class="relative text-xl/7 text-white before:absolute before:-translate-x-full before:content-['“'] after:absolute after:content-['”']">
                      The Largest International Education Provider in Pakistan</p>
                  </blockquote>
                  <figcaption class="mt-6 border-t border-white/20 pt-6">
                    <p class="text-sm/6 font-medium text-white">Blackstone International Teaching Centre</p>
                    <p class="text-sm/6 font-medium"><span
                        class="bg-gradient-to-r from-[#fff1be] from-[28%] via-[#ee87cb] via-[70%] to-[#b060ff] bg-clip-text text-transparent">CEO,
                        Dr. Mary Stiasny</span></p>
                  </figcaption>
                </figure>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>
<script setup>
import { ref,onMounted } from 'vue';
import { RadioGroup, RadioGroupOption } from '@headlessui/vue'
import { CheckIcon } from '@heroicons/vue/20/solid'
import backdrop from '../icon/backdrop.vue';
import Eye from '../icon/eye.vue';
import crossEye from '../icon/crossEye.vue';
import facebook from '../icon/facebook.vue';
import google from '../icon/google.vue';
import mail from '../icon/mail.vue';
const email = ref('');
const password = ref('');
const isPasswordVisible = ref(false);
const loginError = ref('');
const emailError = ref('');
const passwordError = ref('');
const isDarkMode = ref(false);

const frequencies = ref([
  { label: 'Student', value: 'monthly' },
  { label: 'Admin', value: 'admin' },
]);
const frequency = ref(frequencies.value[0]); // Default value
const mockUsers = [
  { email: 'student@example.com', password: 'student123', role: 'Student' },
  { email: 'admin@example.com', password: 'admin123', role: 'Admin' },
];

const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value;
  if (isDarkMode.value) {
    document.documentElement.classList.add('dark');
  } else {
    document.documentElement.classList.remove('dark');
  }
  localStorage.setItem('darkMode', isDarkMode.value);
};

// Initialize dark mode based on localStorage
onMounted(() => {
  isDarkMode.value = localStorage.getItem('darkMode') === 'true';
  if (isDarkMode.value) {
    document.documentElement.classList.add('dark');
  }
});

const validateEmail = () => {
  emailError.value = email.value ? '' : 'Email is required.';
};

const validatePassword = () => {
  passwordError.value = password.value.length < 6 ? 'Password must be at least 6 characters long.' : '';
};

const togglePasswordVisibility = () => {
  isPasswordVisible.value = !isPasswordVisible.value;
};

const handleSubmit = () => {
  loginError.value = ''; // Clear previous error messages
  validateEmail();
  validatePassword();
  if (emailError.value || passwordError.value) return; // Prevent submission if there are errors

  const user = mockUsers.find((user) => user.email === email.value && user.password === password.value);
  if (user) {
    // Simulate role-based redirection
    if (user.role === 'Admin') {
      // Redirect to Admin Dashboard (replace with actual routing logic)
      alert('Login Successful. Redirecting to Admin Dashboard...');
    } else {
      // Redirect to Student Dashboard (replace with actual routing logic)
      alert('Login Successful. Redirecting to Student Dashboard...');
    }
  } else {
    loginError.value = 'Invalid email or password.';
  }
};
</script>

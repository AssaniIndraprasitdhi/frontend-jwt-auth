<template>
  <div class="min-h-screen font-sans bg-cover bg-center flex items-center justify-center px-4"
    style="background-image: url('/background.jpg')">
    <!-- ✅ Overlay Loading -->
    <div v-if="loading" class="absolute inset-0 bg-black/60 backdrop-blur-sm flex items-center justify-center z-50">
      <svg class="animate-spin h-10 w-10 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4" />
        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8v8z" />
      </svg>
    </div>

    <div class="bg-[#1f1f1f]/90 backdrop-blur-md p-8 rounded-2xl shadow-2xl w-full max-w-sm text-white">
      <!-- Logo -->
      <div class="flex justify-center mb-4">
        <img src="/logo.png" alt="Logo" />
      </div>

      <!-- Welcome -->
      <h2 class="text-2xl font-bold text-center">Welcome Users</h2>

      <!-- Form -->
      <div class="mt-6 space-y-4">
        <!-- Email Field -->
        <div class="flex items-center bg-[#2a2a2a] border border-gray-700 rounded-md px-3 py-2">
          <Mail class="h-5 w-5 text-gray-400 mr-2" />
          <input v-model="email" type="email" placeholder="Email address"
            class="flex-1 bg-transparent text-white placeholder-gray-400 focus:outline-none" />
        </div>

        <!-- Password Field -->
        <div class="flex items-center bg-[#2a2a2a] border border-gray-700 rounded-md px-3 py-2">
          <Lock class="h-5 w-5 text-gray-400 mr-2" />
          <input v-model="password" type="password" placeholder="Password"
            class="flex-1 bg-transparent text-white placeholder-gray-400 focus:outline-none" />
        </div>

        <p class="text-sm text-gray-400 text-center mt-1">
          Don't have an account yet?
          <a @click="goToRegister" class="text-blue-500 hover:underline cursor-pointer">Sign up</a>
        </p>

        <!-- Login Button -->
        <button @click="handleLogin" :disabled="loading"
          class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 rounded-md transition duration-200">
          <span v-if="!loading">Login</span>
          <span v-else>Logging in...</span>
        </button>

        <!-- Error Message -->
        <p v-if="error" class="text-sm text-red-400 text-center mt-2">{{ error }}</p>
      </div>

      <!-- Divider -->
      <div class="flex items-center my-6">
        <div class="flex-grow border-t border-gray-700"></div>
        <span class="mx-3 text-gray-500 text-sm">or</span>
        <div class="flex-grow border-t border-gray-700"></div>
      </div>

      <!-- Social Buttons -->
      <div class="flex gap-2">
        <button
          class="flex-1 bg-[#2a2a2a] py-2 rounded-md flex items-center justify-center hover:bg-gray-700 transition">
          <img src="/apple.png" class="h-5" alt="Apple" />
        </button>
        <button
          class="flex-1 bg-[#2a2a2a] py-2 rounded-md flex items-center justify-center hover:bg-gray-700 transition">
          <img src="/google.png" class="h-5" alt="Google" />
        </button>
        <button
          class="flex-1 bg-[#2a2a2a] py-2 rounded-md flex items-center justify-center hover:bg-gray-700 transition">
          <img src="/x.png" class="h-5" alt="X" />
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { useAuthStore } from '../store/auth'
import { Mail, Lock } from 'lucide-vue-next'

const email = ref('')
const password = ref('')
const error = ref('')
const loading = ref(false)

const router = useRouter()
const auth = useAuthStore()

const handleLogin = async () => {
  loading.value = true
  error.value = ''
  try {
    await auth.login(email.value, password.value)
    setTimeout(() => {
      router.push('/dashboard')
    }, 800)
  } catch (err) {
    error.value = 'Invalid credentials'
    loading.value = false
  }
}

const goToRegister = () => {
  loading.value = true
  setTimeout(() => {
    router.push('/register')
  }, 400) 
}

</script>

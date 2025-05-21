<template>
  <div
    class="relative min-h-screen font-sans bg-cover bg-center flex items-center justify-center px-4"
    style="background-image: url('/background.jpg')"
  >
    <!-- 🔄 Loading Overlay -->
    <div v-if="loading" class="absolute inset-0 bg-black/60 backdrop-blur-sm flex items-center justify-center z-50">
      <svg class="animate-spin h-10 w-10 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4" />
        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8v8z" />
      </svg>
    </div>

    <!-- Form Card -->
    <div class="bg-[#1f1f1f]/90 backdrop-blur-md p-8 rounded-2xl shadow-2xl w-full max-w-sm text-white z-10">
      <!-- Logo -->
      <div class="flex justify-center mb-4">
        <img src="/logo.png" alt="Logo"/>
      </div>

      <h2 class="text-2xl font-bold text-center">Create an Account</h2>

      <!-- Form -->
      <div class="mt-6 space-y-4">
        <!-- Username -->
        <div class="flex items-center bg-[#2a2a2a] border border-gray-700 rounded-md px-3 py-2">
          <User class="h-5 w-5 text-gray-400 mr-2" />
          <input
            v-model="username"
            type="text"
            placeholder="Username"
            class="flex-1 bg-transparent text-white placeholder-gray-400 focus:outline-none"
          />
        </div>

        <!-- Email -->
        <div class="flex items-center bg-[#2a2a2a] border border-gray-700 rounded-md px-3 py-2">
          <Mail class="h-5 w-5 text-gray-400 mr-2" />
          <input
            v-model="email"
            type="email"
            placeholder="Email address"
            class="flex-1 bg-transparent text-white placeholder-gray-400 focus:outline-none"
          />
        </div>

        <!-- Password -->
        <div class="flex items-center bg-[#2a2a2a] border border-gray-700 rounded-md px-3 py-2">
          <Lock class="h-5 w-5 text-gray-400 mr-2" />
          <input
            v-model="password"
            type="password"
            placeholder="Password"
            class="flex-1 bg-transparent text-white placeholder-gray-400 focus:outline-none"
          />
        </div>

        <!-- Register Button -->
        <button
          @click="handleRegister"
          :disabled="loading"
          class="w-full bg-green-600 hover:bg-green-700 text-white font-semibold py-2 rounded-md transition duration-200"
        >
          <span v-if="!loading">Register</span>
          <span v-else>Registering...</span>
        </button>

        <!-- Messages -->
        <p v-if="success" class="text-sm text-green-400 text-center mt-2">Register successful! 🎉</p>
        <p v-if="error" class="text-sm text-red-400 text-center mt-2">{{ error }}</p>
      </div>

      <!-- Link to Login -->
      <p class="text-sm text-gray-400 text-center mt-6">
        Already have an account?
        <a @click="goToLogin" class="text-blue-500 hover:underline cursor-pointer">Sign in</a>
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { useAuthStore } from '../store/auth'

// Lucide icons
import { User, Mail, Lock } from 'lucide-vue-next'

const username = ref('')
const email = ref('')
const password = ref('')
const loading = ref(false)
const error = ref('')
const success = ref(false)

const router = useRouter()
const auth = useAuthStore()

const handleRegister = async () => {
  loading.value = true
  error.value = ''
  try {
    await auth.register(username.value, email.value, password.value)
    success.value = true
    setTimeout(() => {
      router.push('/login')
    }, 1000)
  } catch (err) {
    error.value = 'Registration failed'
  } finally {
    loading.value = false
  }
}

const goToLogin = () => {
  loading.value = true
  setTimeout(() => {
    router.push('/login')
  }, 500)
}
</script>

<template>
  <div
    class="min-h-screen font-sans bg-cover bg-center flex items-center justify-center px-4"
    style="background-image: url('/background.jpg')"
  >
    <div class="bg-[#1f1f1f]/90 backdrop-blur-md p-8 rounded-2xl shadow-2xl w-full max-w-2xl text-white">
      <div class="flex items-center justify-between mb-6">
        <div class="flex items-center gap-3">
          <UserCheck class="h-6 w-6 text-green-400" />
          <h1 class="text-2xl font-bold">Welcome to your Dashboard</h1>
        </div>
        <button
          @click="logout"
          class="flex items-center gap-1 px-4 py-2 bg-red-600 hover:bg-red-700 text-white rounded transition"
        >
          <LogOut class="h-5 w-5" />
          Logout
        </button>
      </div>

      <p class="text-gray-300">
        You are now logged in with <span class="text-blue-400 font-semibold">JWT Auth</span>.
      </p>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
import { useAuthStore } from '../store/auth'

// Lucide icons
import { LogOut, UserCheck } from 'lucide-vue-next'

const auth = useAuthStore()
const router = useRouter()

const logout = () => {
  auth.logout()
  router.push('/login')
}
</script>

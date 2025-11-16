<script setup lang="ts">
import { useRouter } from 'vue-router'
import Button from '@/components/ui/button/Button.vue'

const router = useRouter()

const goHome = () => {
  router.push('/')
}

const goBack = () => {
  router.back()
}
</script>

<template>
  <div class="min-h-screen flex items-center justify-center bg-linear-to-b from-gray-50 to-white px-4">
    <div class="text-center max-w-2xl">
      <!-- 404 Illustration -->
      <div class="mb-8">
        <h1 class="text-9xl font-bold text-blue-600 mb-4">404</h1>
        <div class="text-6xl mb-4">🏍️</div>
      </div>

      <!-- Message -->
      <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
        Page Not Found
      </h2>
      <p class="text-lg text-gray-600 mb-8">
        Looks like you've taken a wrong turn. The page you're looking for doesn't exist or has been moved.
      </p>

      <!-- Action Buttons -->
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <Button size="lg" @click="goHome" class="px-8">
          Go to Home
        </Button>
        <Button size="lg" variant="outline" @click="goBack" class="px-8">
          Go Back
        </Button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>

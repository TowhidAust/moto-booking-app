<script setup lang="ts">
import { useRouter } from 'vue-router'
import { Button } from '@/components/ui/button'
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/components/ui/card'

const router = useRouter()

const navigateToServiceCenters = () => {
  router.push('/service-centers')
}

const features = [
  {
    title: 'Easy Booking',
    description: 'Book your motorcycle service in just a few clicks',
    icon: '📅'
  },
  {
    title: 'Trusted Centers',
    description: 'Access verified and certified service centers',
    icon: '✓'
  },
  {
    title: 'Quick Service',
    description: 'Get your motorcycle serviced with minimal wait time',
    icon: '⚡'
  }
]
</script>

<template>
  <div class="min-h-screen bg-linear-to-b from-gray-50 to-white">
    <!-- Hero Section -->
    <div class="container mx-auto px-4 py-16 md:py-24">
      <div class="text-center max-w-3xl mx-auto">
        <h1 class="text-4xl md:text-6xl font-bold text-gray-900 mb-6">
          Motorcycle Service
          <span class="text-blue-600">Made Simple</span>
        </h1>
        <p class="text-lg md:text-xl text-gray-600 mb-8">
          Book appointments with trusted service centers near you. <br /> Fast, reliable, and hassle-free.
        </p>
        <Button @click="navigateToServiceCenters" size="lg" class="text-lg px-8 py-6 h-auto">
          Find Service Centers
        </Button>
      </div>
    </div>

    <!-- Features Section -->
    <div class="container mx-auto px-4 py-16">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-5xl mx-auto">
        <Card v-for="feature in features" :key="feature.title" class="text-center hover:shadow-lg transition-shadow">
          <CardHeader>
            <div class="text-4xl mb-4">{{ feature.icon }}</div>
            <CardTitle class="text-xl">{{ feature.title }}</CardTitle>
          </CardHeader>
          <CardContent>
            <CardDescription class="text-base">{{ feature.description }}</CardDescription>
          </CardContent>
        </Card>
      </div>
    </div>

    <!-- CTA Section -->
    <div class="container mx-auto px-4 py-16">
      <div class="max-w-2xl mx-auto text-center bg-blue-50 rounded-2xl p-8 md:p-12">
        <h2 class="text-2xl md:text-3xl font-bold text-gray-900 mb-4">
          Ready to service your motorcycle?
        </h2>
        <p class="text-gray-600 mb-6">
          Browse available service centers and book your appointment today.
        </p>
        <Button @click="navigateToServiceCenters" variant="outline" size="lg" class="text-lg px-8 py-6 h-auto">
          Get Started
        </Button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
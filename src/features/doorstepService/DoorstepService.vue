<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import Card from '@/components/ui/card/Card.vue'
import CardContent from '@/components/ui/card/CardContent.vue'
import CardHeader from '@/components/ui/card/CardHeader.vue'
import CardTitle from '@/components/ui/card/CardTitle.vue'
import CardDescription from '@/components/ui/card/CardDescription.vue'
import Button from '@/components/ui/button/Button.vue'
import {
  Speaker,
  Wrench,
  Droplets,
  Search,
  Link2,
  Battery,
  Gauge,
  Lightbulb,
  Wind,
  Sparkles,
  Shield,
  Package,
  Home
} from 'lucide-vue-next'

const router = useRouter()

const doorstepServices = ref([
  {
    id: 1,
    name: 'Horn Replacement',
    icon: Speaker,
    description: 'Replace your bike horn with a new one at your doorstep',
    duration: '15-20 min',
    price: '৳350',
    popular: false,
  },
  {
    id: 2,
    name: 'Handle Riser Installation',
    icon: Wrench,
    description: 'Professional installation of handle risers for better riding comfort',
    duration: '30-45 min',
    price: '৳500',
    popular: false,
  },
  {
    id: 3,
    name: 'Bike Wash at Home',
    icon: Droplets,
    description: 'Complete bike washing and cleaning service at your location',
    duration: '45-60 min',
    price: '৳300',
    popular: true,
  },
  {
    id: 4,
    name: 'Bike Inspection',
    icon: Search,
    description: 'Comprehensive safety and maintenance inspection',
    duration: '30-40 min',
    price: '৳400',
    popular: false,
  },
  {
    id: 5,
    name: 'Chain Set Replacement',
    icon: Link2,
    description: 'Replace worn-out chain and sprocket set',
    duration: '1-1.5 hours',
    price: '৳800',
    popular: false,
  },
  {
    id: 6,
    name: 'Battery Replacement',
    icon: Battery,
    description: 'Quick battery replacement service at your doorstep',
    duration: '15-20 min',
    price: '৳450',
    popular: false,
  },
  {
    id: 7,
    name: 'Oil Change Service',
    icon: Gauge,
    description: 'Engine oil and filter replacement at your home',
    duration: '30-45 min',
    price: '৳600',
    popular: true,
  },
  {
    id: 8,
    name: 'Light Bulb Replacement',
    icon: Lightbulb,
    description: 'Replace headlight, taillight, or indicator bulbs',
    duration: '10-15 min',
    price: '৳200',
    popular: false,
  },
  {
    id: 9,
    name: 'Air Filter Cleaning',
    icon: Wind,
    description: 'Clean or replace air filter for better performance',
    duration: '20-30 min',
    price: '৳350',
    popular: false,
  },
  {
    id: 10,
    name: 'Chain Cleaning & Lubrication',
    icon: Sparkles,
    description: 'Deep chain cleaning and proper lubrication',
    duration: '25-35 min',
    price: '৳250',
    popular: true,
  },
  {
    id: 11,
    name: 'Brake Pad Replacement',
    icon: Shield,
    description: 'Replace front or rear brake pads for safety',
    duration: '40-50 min',
    price: '৳700',
    popular: false,
  },
  {
    id: 12,
    name: 'Accessories Installation',
    icon: Package,
    description: 'Install phone holders, mirrors, crash guards, etc.',
    duration: '30-60 min',
    price: '৳400',
    popular: false,
  },
])

const selectedService = ref<number | null>(null)

const selectService = (serviceId: number) => {
  selectedService.value = serviceId
}

const bookService = () => {
  if (selectedService.value) {
    const service = doorstepServices.value.find(s => s.id === selectedService.value)
    alert(`Booking ${service?.name} - Proceeding to schedule`)
    // router.push('/schedule')
  } else {
    alert('Please select a service first')
  }
}

const goBack = () => {
  router.push('/')
}
</script>

<template>
  <div>
    <!-- Back Button -->
    <Button variant="outline" @click="goBack" class="mb-6">
      ← Back to Home
    </Button>

    <!-- Header -->
    <div class="mb-8 text-center max-w-3xl mx-auto">
      <div class="flex justify-center mb-4">
        <div class="p-4 bg-blue-100 rounded-full">
          <Home class="w-12 h-12 text-blue-600" />
        </div>
      </div>
      <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-3">Doorstep Service</h1>
      <p class="text-lg text-gray-600">
        Get your motorcycle serviced at your home. Select a service package and schedule a visit.
      </p>
    </div>

    <!-- Service Packages Grid -->
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6 mb-8">
      <Card v-for="service in doorstepServices" :key="service.id" :class="[
        'cursor-pointer transition-all duration-300 relative hover:shadow-lg',
        selectedService === service.id
          ? 'ring-2 ring-blue-500 border-blue-500 shadow-lg'
          : 'hover:border-blue-200',
      ]" @click="selectService(service.id)">
        <div v-if="service.popular"
          class="absolute -top-2 -right-2 bg-green-500 text-white px-2 py-1 rounded-full text-xs font-semibold">
          Popular
        </div>

        <CardHeader class="pb-3">
          <div class="flex flex-col items-center text-center mb-2">
            <div class="p-3 bg-blue-100 rounded-full mb-3">
              <component :is="service.icon" class="w-8 h-8 text-blue-600" />
            </div>
            <CardTitle class="text-lg leading-tight mb-2">{{ service.name }}</CardTitle>
            <CardDescription class="text-sm">{{ service.description }}</CardDescription>
          </div>
        </CardHeader>

        <CardContent class="space-y-3">
          <div class="flex items-center justify-between text-sm border-t border-b py-2">
            <span class="text-gray-600">Duration</span>
            <span class="font-medium">{{ service.duration }}</span>
          </div>

          <div class="flex items-center justify-between">
            <span class="text-sm text-gray-600">Price</span>
            <span class="text-2xl font-bold text-blue-600">{{ service.price }}</span>
          </div>

          <Button :variant="selectedService === service.id ? 'default' : 'outline'" class="w-full"
            @click.stop="selectService(service.id)">
            {{ selectedService === service.id ? 'Selected' : 'Select' }}
          </Button>
        </CardContent>
      </Card>
    </div>

    <!-- Book Service Button -->
    <div class="flex justify-center pb-8">
      <Button size="lg" class="px-12 py-6 text-lg h-auto" :disabled="!selectedService" @click="bookService">
        Book Selected Service
      </Button>
    </div>

    <!-- Info Section -->
    <div class="max-w-4xl mx-auto">
      <Card class="bg-blue-50 border-blue-200">
        <CardContent class="py-6">
          <h3 class="font-bold text-lg text-gray-900 mb-3">How It Works</h3>
          <div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-sm">
            <div class="flex gap-3">
              <div
                class="shrink-0 w-8 h-8 bg-blue-600 text-white rounded-full flex items-center justify-center font-bold">
                1
              </div>
              <div>
                <p class="font-semibold text-gray-900">Select Service</p>
                <p class="text-gray-600">Choose from available doorstep services</p>
              </div>
            </div>
            <div class="flex gap-3">
              <div
                class="shrink-0 w-8 h-8 bg-blue-600 text-white rounded-full flex items-center justify-center font-bold">
                2
              </div>
              <div>
                <p class="font-semibold text-gray-900">Schedule Visit</p>
                <p class="text-gray-600">Pick your preferred date and time</p>
              </div>
            </div>
            <div class="flex gap-3">
              <div
                class="shrink-0 w-8 h-8 bg-blue-600 text-white rounded-full flex items-center justify-center font-bold">
                3
              </div>
              <div>
                <p class="font-semibold text-gray-900">Get Service</p>
                <p class="text-gray-600">Our expert will arrive at your location</p>
              </div>
            </div>
          </div>
        </CardContent>
      </Card>
    </div>
  </div>
</template>

<style scoped></style>

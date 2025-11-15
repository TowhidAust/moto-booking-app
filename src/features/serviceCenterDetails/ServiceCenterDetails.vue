<script setup lang="ts">
import { useRoute, useRouter } from 'vue-router'
import { ref } from 'vue'
import Card from '@/components/ui/card/Card.vue'
import CardContent from '@/components/ui/card/CardContent.vue'
import CardHeader from '@/components/ui/card/CardHeader.vue'
import CardTitle from '@/components/ui/card/CardTitle.vue'
import CardDescription from '@/components/ui/card/CardDescription.vue'
import Button from '@/components/ui/button/Button.vue'
import { MapPin, Phone, Star, Clock, Wrench, Settings, Zap, Speaker, Package } from 'lucide-vue-next'

const route = useRoute()
const router = useRouter()
const serviceCenterId = route.params.id

// Mock data - in real app, fetch based on serviceCenterId
const serviceCenter = ref({
  id: Number(serviceCenterId),
  name: 'Bikers Headquarter',
  address: '123 Main St, Cityville',
  phone: '555-1234',
  rating: 4.8,
  reviews: 124,
  hours: 'Mon-Sat: 9:00 AM - 6:00 PM',
})

const servicePackages = ref([
  {
    id: 1,
    name: 'Regular Maintenance',
    icon: Wrench,
    description: 'Basic oil change, chain lubrication, and general inspection',
    duration: '1-2 hours',
    price: '৳1,500',
    features: ['Engine oil replacement', 'Chain cleaning & lubrication', 'Brake inspection', 'Tire pressure check'],
  },
  {
    id: 2,
    name: 'Master Servicing',
    icon: Settings,
    description: 'Complete bike overhaul with deep cleaning and part replacement',
    duration: '4-6 hours',
    price: '৳5,000',
    features: ['Full engine service', 'Carburetor cleaning', 'Brake pad replacement', 'Complete bike wash', 'All fluid replacements'],
    popular: true,
  },
  {
    id: 3,
    name: 'Pay As You Go',
    icon: Zap,
    description: 'Flexible service based on your specific needs',
    duration: 'Variable',
    price: 'Custom',
    features: ['Choose specific repairs', 'Pay only for what you need', 'Expert diagnosis', 'Transparent pricing'],
  },
  {
    id: 4,
    name: 'Accessories Installation',
    icon: Package,
    description: 'Professional installation of bike accessories and upgrades',
    duration: '30 min - 2 hours',
    price: '৳500+',
    features: ['Phone holders', 'USB chargers', 'Crash guards', 'LED lights', 'Luggage carriers'],
  },
  {
    id: 5,
    name: 'Horn Replacement',
    icon: Speaker,
    description: 'Quick horn replacement or repair service',
    duration: '15-30 minutes',
    price: '৳300',
    features: ['Original horn installation', 'Wiring check', 'Sound quality test', 'Waterproof connection'],
  },
  {
    id: 6,
    name: 'Quick Check-up',
    icon: Clock,
    description: 'Fast diagnostic check before long rides',
    duration: '30 minutes',
    price: '৳500',
    features: ['Brake test', 'Light inspection', 'Tire condition check', 'Fluid levels', 'Basic safety check'],
  },
])

const selectedPackage = ref<number | null>(null)

const selectPackage = (packageId: number) => {
  selectedPackage.value = packageId
}

const bookService = () => {
  if (selectedPackage.value) {
    const pkg = servicePackages.value.find(p => p.id === selectedPackage.value)
    alert(`Booking confirmed for ${pkg?.name} at ${serviceCenter.value.name}`)
  } else {
    alert('Please select a service package first')
  }
}

const goBack = () => {
  router.push('/service-centers')
}
</script>

<template>
  <div class="bg-gray-50">
    <div>
      <!-- Back Button -->
      <Button variant="outline" @click="goBack" class="mb-6">
        ← Back to Service Centers
      </Button>

      <!-- Service Center Info -->
      <Card class="mb-8">
        <CardHeader>
          <div class="flex items-start justify-between flex-wrap gap-4">
            <div>
              <CardTitle class="text-3xl mb-2">{{ serviceCenter.name }}</CardTitle>
              <div class="flex items-center gap-1 mb-3">
                <Star class="w-5 h-5 fill-yellow-400 text-yellow-400" />
                <span class="text-lg font-medium text-gray-900">{{ serviceCenter.rating }}</span>
                <span class="text-gray-500">({{ serviceCenter.reviews }} reviews)</span>
              </div>
            </div>
          </div>
        </CardHeader>
        <CardContent class="space-y-3">
          <div class="flex items-start gap-2 text-gray-600">
            <MapPin class="w-5 h-5 mt-0.5 shrink-0 text-blue-600" />
            <span>{{ serviceCenter.address }}</span>
          </div>
          <div class="flex items-center gap-2 text-gray-600">
            <Phone class="w-5 h-5 shrink-0 text-blue-600" />
            <span>{{ serviceCenter.phone }}</span>
          </div>
          <div class="flex items-center gap-2 text-gray-600">
            <Clock class="w-5 h-5 shrink-0 text-blue-600" />
            <span>{{ serviceCenter.hours }}</span>
          </div>
        </CardContent>
      </Card>

      <!-- Service Packages Section -->
      <div class="mb-6">
        <h2 class="text-2xl font-bold text-gray-900 mb-2">Service Packages</h2>
        <p class="text-gray-600">Choose a service package that fits your needs</p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-8">
        <Card 
          v-for="pkg in servicePackages" :key="pkg.id" :class="[
          'cursor-pointer relative',
          selectedPackage === pkg.id
            ? 'ring-2 ring-blue-500 border-blue-500 shadow-lg'
            : 'hover:shadow-lg hover:border-blue-200',
        ]" @click="selectPackage(pkg.id)">
          <div v-if="pkg.popular"
            class="absolute -top-3 -right-3 bg-blue-600 text-white px-3 py-1 rounded-full text-xs font-semibold">
            Popular
          </div>

          <CardHeader class="pb-3">
            <div class="flex items-start gap-3">
              <div class="p-2 bg-blue-100 rounded-lg">
                <component :is="pkg.icon" class="w-6 h-6 text-blue-600" />
              </div>
              <div class="flex-1">
                <CardTitle class="text-xl mb-1">{{ pkg.name }}</CardTitle>
                <CardDescription>{{ pkg.description }}</CardDescription>
              </div>
            </div>
          </CardHeader>

          <CardContent class="space-y-4">
            <div class="flex items-center justify-between py-2 border-t border-b">
              <div class="flex items-center gap-2 text-sm text-gray-600">
                <Clock class="w-4 h-4" />
                <span>{{ pkg.duration }}</span>
              </div>
              <div class="text-2xl font-bold text-blue-600">{{ pkg.price }}</div>
            </div>

            <div>
              <p class="text-sm font-semibold text-gray-700 mb-2">Includes:</p>
              <ul class="space-y-1">
                <li v-for="(feature, index) in pkg.features" :key="index"
                  class="text-sm text-gray-600 flex items-start gap-2">
                  <span class="text-green-600 mt-0.5">✓</span>
                  <span>{{ feature }}</span>
                </li>
              </ul>
            </div>

            <Button :variant="selectedPackage === pkg.id ? 'default' : 'outline'" class="w-full"
              @click.stop="selectPackage(pkg.id)">
              {{ selectedPackage === pkg.id ? 'Selected' : 'Select Package' }}
            </Button>
          </CardContent>
        </Card>
      </div>

      <!-- Book Button -->
      <div class="flex justify-center">
        <Button size="lg" class="px-12 py-6 text-lg h-auto" :disabled="!selectedPackage" @click="bookService">
          Book Selected Service
        </Button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
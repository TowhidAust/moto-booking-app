<script setup lang="ts">
import Card from '@/components/ui/card/Card.vue'
import CardContent from '@/components/ui/card/CardContent.vue'
import CardHeader from '@/components/ui/card/CardHeader.vue'
import CardTitle from '@/components/ui/card/CardTitle.vue'
import Button from '@/components/ui/button/Button.vue'
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { MapPin, Phone, Star } from 'lucide-vue-next'

const serviceCenters = ref([
  {
    id: 1,
    name: 'Bikers Headquarter',
    address: '123 Main St, Cityville',
    phone: '555-1234',
    rating: 4.8,
    reviews: 124,
  },
  {
    id: 2,
    name: 'Moto Mechs Bangladesh',
    address: '456 Elm St, Cityville',
    phone: '555-5678',
    rating: 4.6,
    reviews: 98,
  },
  {
    id: 3,
    name: 'Bike Care Center',
    address: '789 Oak St, Cityville',
    phone: '555-9012',
    rating: 4.9,
    reviews: 156,
  },
  {
    id: 4,
    name: 'Speedy Service Hub',
    address: '321 Pine St, Cityville',
    phone: '555-3456',
    rating: 4.5,
    reviews: 87,
  },
  {
    id: 5,
    name: 'Ride Ready Workshop',
    address: '654 Maple St, Cityville',
    phone: '555-7890',
    rating: 4.7,
    reviews: 112,
  },
  {
    id: 6,
    name: 'Two-Wheel Techs',
    address: '987 Cedar St, Cityville',
    phone: '555-2345',
    rating: 4.8,
    reviews: 143,
  },
  {
    id: 7,
    name: 'Cycle Solutions',
    address: '147 Spruce St, Cityville',
    phone: '555-6789',
    rating: 4.4,
    reviews: 76,
  },
  {
    id: 8,
    name: 'Urban Moto Service',
    address: '258 Birch St, Cityville',
    phone: '555-0123',
    rating: 4.7,
    reviews: 91,
  },
])
const router = useRouter();

const bookServiceCenter = (id: number) => {
  const center = serviceCenters.value.find((sc) => sc.id === id)
  if (center) {
    router.replace({ name: 'service-center-details', params: { id: id } });
  }
}

</script>
<template>
  <div>
    <div class="mb-8">
      <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-2">Service Centers</h1>
      <p class="text-gray-600">Find and book your nearest motorcycle service center</p>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <Card v-for="serviceCenter in serviceCenters" :key="serviceCenter.id"
        class="hover:shadow-xl transition-all duration-300 cursor-pointer border-2 hover:border-blue-200"
        @click="bookServiceCenter(serviceCenter.id)">
        <CardHeader class="pb-3">
          <div class="flex items-start justify-between">
            <CardTitle class="text-xl font-semibold leading-tight">
              {{ serviceCenter.name }}
            </CardTitle>
          </div>
          <div class="flex items-center gap-1 mt-2">
            <Star class="w-4 h-4 fill-yellow-400 text-yellow-400" />
            <span class="text-sm font-medium text-gray-900">{{ serviceCenter.rating }}</span>
            <span class="text-sm text-gray-500">({{ serviceCenter.reviews }} reviews)</span>
          </div>
        </CardHeader>

        <CardContent class="space-y-3">
          <div class="flex items-start gap-2 text-gray-600">
            <MapPin class="w-4 h-4 mt-0.5 shrink-0 text-blue-600" />
            <span class="text-sm">{{ serviceCenter.address }}</span>
          </div>

          <div class="flex items-center gap-2 text-gray-600">
            <Phone class="w-4 h-4 shrink-0 text-blue-600" />
            <span class="text-sm">{{ serviceCenter.phone }}</span>
          </div>

          <div class="pt-2">
            <Button class="w-full" variant="default" @click.stop="bookServiceCenter(serviceCenter.id)">
              Book Appointment
            </Button>
          </div>
        </CardContent>
      </Card>
    </div>
  </div>
</template>

<style scoped></style>
<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { Button } from '@/components/ui/button'
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card'
import { 
  Calendar, 
  Clock, 
  MapPin, 
  Wrench, 
  CheckCircle2, 
  AlertCircle,
  History,
  CreditCard,
  Bike
} from 'lucide-vue-next'

const router = useRouter()

// User info
const user = ref({
  name: 'Towhid Ahmed',
  totalBookings: 12,
  completedServices: 10,
  upcomingServices: 1,
  lastService: '2 weeks ago'
})

// Upcoming booking
const upcomingBooking = ref({
  id: 1,
  serviceCenter: 'Bikers Headquarter',
  serviceName: 'Regular Maintenance',
  address: '123 Main St, Cityville',
  date: 'November 18, 2025',
  time: '10:00 AM',
  price: 1500,
  status: 'confirmed'
})

// Recent bookings history
const recentBookings = ref([
  {
    id: 2,
    serviceCenter: 'Moto Mechs Bangladesh',
    serviceName: 'Oil Change Service',
    date: 'November 5, 2025',
    status: 'completed',
    amount: 600
  },
  {
    id: 3,
    serviceCenter: 'Bike Care Center',
    serviceName: 'Chain Cleaning',
    date: 'October 28, 2025',
    status: 'completed',
    amount: 250
  },
  {
    id: 4,
    serviceCenter: 'Two-Wheel Techs',
    serviceName: 'Brake Pad Replacement',
    date: 'October 15, 2025',
    status: 'completed',
    amount: 700
  }
])

// Quick stats
const stats = ref([
  {
    label: 'Total Bookings',
    value: '12',
    icon: Calendar,
    color: 'text-blue-600',
    bg: 'bg-blue-100'
  },
  {
    label: 'Completed',
    value: '10',
    icon: CheckCircle2,
    color: 'text-green-600',
    bg: 'bg-green-100'
  },
  {
    label: 'Upcoming',
    value: '1',
    icon: Clock,
    color: 'text-orange-600',
    bg: 'bg-orange-100'
  },
  {
    label: 'Total Spent',
    value: '৳8,450',
    icon: CreditCard,
    color: 'text-purple-600',
    bg: 'bg-purple-100'
  }
])

const viewBookingDetails = (bookingId: number) => {
  alert(`View details for booking #${bookingId}`)
}

const bookNewService = () => {
  router.push('/service-centers')
}

const bookDoorstepService = () => {
  router.push('/doorstep-service')
}
</script>

<template>

    <div>
      <!-- Welcome Header -->
      <div class="mb-6">
        <h1 class="text-2xl md:text-3xl font-bold text-gray-900 mb-1">
          Welcome back, {{ user.name }}! 👋
        </h1>
        <p class="text-gray-600">Here's your service dashboard</p>
      </div>

      <!-- Quick Stats -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-6">
        <Card v-for="stat in stats" :key="stat.label" class="hover:shadow-md transition-shadow">
          <CardContent class="p-4">
            <div class="flex items-center gap-3">
              <div :class="['p-2 rounded-lg', stat.bg]">
                <component :is="stat.icon" :class="['w-5 h-5', stat.color]" />
              </div>
              <div>
                <p class="text-xs text-gray-600">{{ stat.label }}</p>
                <p class="text-xl font-bold text-gray-900">{{ stat.value }}</p>
              </div>
            </div>
          </CardContent>
        </Card>
      </div>

      <!-- Upcoming Booking -->
      <Card class="mb-6 border-l-4 border-l-blue-600">
        <CardHeader>
          <div class="flex items-center justify-between">
            <CardTitle class="text-xl flex items-center gap-2">
              <AlertCircle class="w-5 h-5 text-blue-600" />
              Upcoming Appointment
            </CardTitle>
            <span class="px-3 py-1 bg-green-100 text-green-700 text-xs font-semibold rounded-full">
              Confirmed
            </span>
          </div>
        </CardHeader>
        <CardContent class="space-y-4">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <div class="flex items-start gap-2 mb-3">
                <Wrench class="w-5 h-5 text-blue-600 mt-0.5" />
                <div>
                  <p class="font-semibold text-gray-900">{{ upcomingBooking.serviceName }}</p>
                  <p class="text-sm text-gray-600">{{ upcomingBooking.serviceCenter }}</p>
                </div>
              </div>
              <div class="flex items-start gap-2 mb-2">
                <MapPin class="w-4 h-4 text-gray-500 mt-0.5" />
                <p class="text-sm text-gray-600">{{ upcomingBooking.address }}</p>
              </div>
            </div>
            <div class="space-y-2">
              <div class="flex items-center gap-2">
                <Calendar class="w-4 h-4 text-gray-500" />
                <span class="text-sm text-gray-600">{{ upcomingBooking.date }}</span>
              </div>
              <div class="flex items-center gap-2">
                <Clock class="w-4 h-4 text-gray-500" />
                <span class="text-sm text-gray-600">{{ upcomingBooking.time }}</span>
              </div>
              <div class="flex items-center gap-2">
                <CreditCard class="w-4 h-4 text-gray-500" />
                <span class="text-sm font-semibold text-gray-900">৳{{ upcomingBooking.price }}</span>
              </div>
            </div>
          </div>
          <div class="flex gap-3 pt-2 border-t">
            <Button variant="default" size="sm" @click="viewBookingDetails(upcomingBooking.id)">
              View Details
            </Button>
            <Button variant="outline" size="sm">
              Reschedule
            </Button>
            <Button variant="outline" size="sm" class="text-red-600 hover:text-red-700">
              Cancel
            </Button>
          </div>
        </CardContent>
      </Card>

      <!-- Quick Actions -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
        <Card class="cursor-pointer hover:shadow-lg transition-shadow border-2 hover:border-blue-300" @click="bookNewService">
          <CardContent class="p-6">
            <div class="flex items-center gap-4">
              <div class="p-3 bg-blue-100 rounded-lg">
                <MapPin class="w-8 h-8 text-blue-600" />
              </div>
              <div class="flex-1">
                <h3 class="font-bold text-lg text-gray-900 mb-1">Book Service Center</h3>
                <p class="text-sm text-gray-600">Find and book nearby service centers</p>
              </div>
            </div>
          </CardContent>
        </Card>

        <Card class="cursor-pointer hover:shadow-lg transition-shadow border-2 hover:border-green-300" @click="bookDoorstepService">
          <CardContent class="p-6">
            <div class="flex items-center gap-4">
              <div class="p-3 bg-green-100 rounded-lg">
                <Bike class="w-8 h-8 text-green-600" />
              </div>
              <div class="flex-1">
                <h3 class="font-bold text-lg text-gray-900 mb-1">Doorstep Service</h3>
                <p class="text-sm text-gray-600">Get service at your home</p>
              </div>
            </div>
          </CardContent>
        </Card>
      </div>

      <!-- Recent Bookings History -->
      <Card>
        <CardHeader>
          <CardTitle class="text-xl flex items-center gap-2">
            <History class="w-5 h-5 text-gray-700" />
            Recent Bookings
          </CardTitle>
        </CardHeader>
        <CardContent>
          <div class="space-y-3">
            <div 
              v-for="booking in recentBookings" 
              :key="booking.id"
              class="flex items-center justify-between p-4 bg-gray-50 rounded-lg hover:bg-gray-100 transition-colors cursor-pointer"
              @click="viewBookingDetails(booking.id)"
            >
              <div class="flex items-start gap-3 flex-1">
                <div class="p-2 bg-green-100 rounded-lg">
                  <CheckCircle2 class="w-5 h-5 text-green-600" />
                </div>
                <div>
                  <p class="font-semibold text-gray-900">{{ booking.serviceName }}</p>
                  <p class="text-sm text-gray-600">{{ booking.serviceCenter }}</p>
                  <p class="text-xs text-gray-500 mt-1">{{ booking.date }}</p>
                </div>
              </div>
              <div class="text-right">
                <p class="font-semibold text-gray-900">৳{{ booking.amount }}</p>
                <span class="text-xs text-green-600 font-medium">Completed</span>
              </div>
            </div>
          </div>
          <Button variant="outline" class="w-full mt-4">
            View All History
          </Button>
        </CardContent>
      </Card>
    </div>
</template>

<style scoped>
h1, h2, h3 {
  font-family: 'Telenor', sans-serif;
}
</style>
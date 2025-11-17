<script setup lang="ts">
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'
import Card from '@/components/ui/card/Card.vue'
import CardContent from '@/components/ui/card/CardContent.vue'
import CardHeader from '@/components/ui/card/CardHeader.vue'
import CardTitle from '@/components/ui/card/CardTitle.vue'
import Button from '@/components/ui/button/Button.vue'
import { Calendar, Clock, CheckCircle2 } from 'lucide-vue-next'

const router = useRouter()

// Current date and next 7 days
const generateDates = () => {
  const dates = []
  const today = new Date()
  for (let i = 0; i < 7; i++) {
    const date = new Date(today)
    date.setDate(today.getDate() + i)
    dates.push({
      id: i,
      date: date,
      day: date.toLocaleDateString('en-US', { weekday: 'short' }),
      dayNum: date.getDate(),
      month: date.toLocaleDateString('en-US', { month: 'short' }),
      fullDate: date.toLocaleDateString('en-US', {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      })
    })
  }
  return dates
}

const availableDates = ref(generateDates())
const selectedDate = ref<number | null>(null)
const selectedTime = ref<string | null>(null)

// Time slots
const timeSlots = ref([
  { id: 1, time: '09:00 AM', available: true },
  { id: 2, time: '10:00 AM', available: true },
  { id: 3, time: '11:00 AM', available: false },
  { id: 4, time: '12:00 PM', available: true },
  { id: 5, time: '01:00 PM', available: true },
  { id: 6, time: '02:00 PM', available: true },
  { id: 7, time: '03:00 PM', available: false },
  { id: 8, time: '04:00 PM', available: true },
  { id: 9, time: '05:00 PM', available: true },
])

const selectDate = (dateId: number) => {
  selectedDate.value = dateId
  selectedTime.value = null // Reset time when date changes
}

const selectTime = (time: string, available: boolean) => {
  if (available) {
    selectedTime.value = time
  }
}

const selectedDateObj = computed(() => {
  return availableDates.value.find(d => d.id === selectedDate.value)
})

const canConfirm = computed(() => {
  return selectedDate.value !== null && selectedTime.value !== null
})

const confirmBooking = () => {
  if (canConfirm.value) {
    // alert(`Booking confirmed for ${selectedDateObj.value?.fullDate} at ${selectedTime.value}`)
    router.push(`/service-center/${router.currentRoute.value.params.id}/payment-checkout`)
  }
}

const goBack = () => {
  router.back()
}
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <div>
      <!-- Back Button -->
      <Button variant="outline" @click="goBack" class="mb-6">
        ← Back
      </Button>

      <!-- Header -->
      <div class="mb-8 text-center">
        <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-2">Schedule Your Service</h1>
        <p class="text-gray-600">Select a date and time slot for your appointment</p>
      </div>

      <!-- Date Selection -->
      <Card class="mb-6">
        <CardHeader>
          <div class="flex items-center gap-2">
            <Calendar class="w-5 h-5 text-blue-600" />
            <CardTitle class="text-xl">Select Date</CardTitle>
          </div>
        </CardHeader>
        <CardContent>
          <div class="grid grid-cols-7 gap-2">
            <button v-for="date in availableDates" :key="date.id" @click="selectDate(date.id)" :class="[
              'flex flex-col items-center p-3 rounded-lg border-2 transition-all duration-200',
              selectedDate === date.id
                ? 'border-blue-600 bg-blue-50 text-blue-600'
                : 'border-gray-200 hover:border-blue-300 hover:bg-gray-50',
            ]">
              <span class="text-xs font-medium">{{ date.day }}</span>
              <span class="text-2xl font-bold my-1">{{ date.dayNum }}</span>
              <span class="text-xs text-gray-500">{{ date.month }}</span>
            </button>
          </div>
          <div v-if="selectedDateObj" class="mt-4 p-3 bg-blue-50 rounded-lg text-center">
            <p class="text-sm text-blue-800 font-medium">
              <CheckCircle2 class="w-4 h-4 inline mr-1" />
              {{ selectedDateObj.fullDate }}
            </p>
          </div>
        </CardContent>
      </Card>

      <!-- Time Slot Selection -->
      <Card class="mb-8">
        <CardHeader>
          <div class="flex items-center gap-2">
            <Clock class="w-5 h-5 text-blue-600" />
            <CardTitle class="text-xl">Select Time Slot</CardTitle>
          </div>
        </CardHeader>
        <CardContent>
          <div v-if="selectedDate === null" class="text-center py-8 text-gray-500">
            Please select a date first
          </div>
          <div v-else class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-3">
            <button v-for="slot in timeSlots" :key="slot.id" @click="selectTime(slot.time, slot.available)"
              :disabled="!slot.available" :class="[
                'p-4 rounded-lg border-2 font-medium transition-all duration-200',
                !slot.available
                  ? 'border-gray-200 bg-gray-100 text-gray-400 cursor-not-allowed line-through'
                  : selectedTime === slot.time
                    ? 'border-blue-600 bg-blue-50 text-blue-600'
                    : 'border-gray-200 hover:border-blue-300 hover:bg-gray-50 cursor-pointer',
              ]">
              {{ slot.time }}
            </button>
          </div>
          <div class="mt-4 flex items-center gap-4 text-sm text-gray-600">
            <div class="flex items-center gap-2">
              <div class="w-4 h-4 border-2 border-blue-600 bg-blue-50 rounded"></div>
              <span>Selected</span>
            </div>
            <div class="flex items-center gap-2">
              <div class="w-4 h-4 border-2 border-gray-200 rounded"></div>
              <span>Available</span>
            </div>
            <div class="flex items-center gap-2">
              <div class="w-4 h-4 border-2 border-gray-200 bg-gray-100 rounded"></div>
              <span>Unavailable</span>
            </div>
          </div>
        </CardContent>
      </Card>

      <!-- Summary & Confirm -->
      <Card v-if="canConfirm" class="bg-blue-50 border-blue-200">
        <CardContent class="py-6">
          <div class="flex flex-col md:flex-row items-center justify-between gap-4">
            <div>
              <p class="text-sm text-gray-600 mb-1">Your Appointment</p>
              <p class="text-lg font-bold text-gray-900">
                {{ selectedDateObj?.fullDate }} at {{ selectedTime }}
              </p>
            </div>
            <Button size="lg" @click="confirmBooking" class="px-8 w-full md:w-auto">
              Confirm Booking
            </Button>
          </div>
        </CardContent>
      </Card>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-family: 'Telenor', sans-serif;
}
</style>

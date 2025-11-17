<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import Card from '@/components/ui/card/Card.vue'
import CardContent from '@/components/ui/card/CardContent.vue'
import CardHeader from '@/components/ui/card/CardHeader.vue'
import CardTitle from '@/components/ui/card/CardTitle.vue'
import Button from '@/components/ui/button/Button.vue'
import { CreditCard, MapPin, Phone, Calendar, Clock, Wrench, ShoppingBag } from 'lucide-vue-next'

const router = useRouter()

// Static booking data
const bookingDetails = ref({
  serviceCenter: 'Bikers Headquarter',
  serviceName: 'Regular Maintenance',
  date: 'Monday, November 18, 2025',
  time: '10:00 AM',
  price: 1500,
  bookingFee: 100,
})

// Static customer data (pre-filled)
const customerInfo = ref({
  name: 'Towhid Ahmed',
  phone: '+880 1712-345678',
  address: '123 Dhanmondi, Dhaka 1209, Bangladesh',
  email: 'towhid@example.com'
})

const paymentMethod = ref('bkash')

const processing = ref(false)

const processPayment = () => {
  processing.value = true
  setTimeout(() => {
    alert('Payment of ৳100 successful! Your booking is confirmed.')
    processing.value = false
    router.push('/')
  }, 2000)
}

const goBack = () => {
  router.back()
}
</script>

<template>
  <div>
    <!-- Back Button -->
    <Button variant="outline" @click="goBack" class="mb-6">
      ← Back
    </Button>

    <!-- Header -->
    <div class="mb-8">
      <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-2">Payment Checkout</h1>
      <p class="text-gray-600">Complete your booking by paying the booking fee</p>
    </div>

    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
      <!-- Main Content - Left Side -->
      <div class="lg:col-span-2 space-y-6">
        <!-- Customer Information -->
        <Card>
          <CardHeader>
            <CardTitle class="text-xl flex items-center gap-2">
              <MapPin class="w-5 h-5 text-blue-600" />
              Customer Information
            </CardTitle>
          </CardHeader>
          <CardContent class="space-y-4">
            <div>
              <label class="text-sm font-medium text-gray-700">Full Name</label>
              <div class="mt-1 p-3 bg-gray-50 rounded-lg border">
                {{ customerInfo.name }}
              </div>
            </div>
            <div>
              <label class="text-sm font-medium text-gray-700 flex items-center gap-2">
                <Phone class="w-4 h-4" />
                Phone Number
              </label>
              <div class="mt-1 p-3 bg-gray-50 rounded-lg border">
                {{ customerInfo.phone }}
              </div>
            </div>
            <div>
              <label class="text-sm font-medium text-gray-700">Email</label>
              <div class="mt-1 p-3 bg-gray-50 rounded-lg border">
                {{ customerInfo.email }}
              </div>
            </div>
            <div>
              <label class="text-sm font-medium text-gray-700 flex items-center gap-2">
                <MapPin class="w-4 h-4" />
                Address
              </label>
              <div class="mt-1 p-3 bg-gray-50 rounded-lg border">
                {{ customerInfo.address }}
              </div>
            </div>
          </CardContent>
        </Card>

        <!-- Payment Method -->
        <Card>
          <CardHeader>
            <CardTitle class="text-xl flex items-center gap-2">
              <CreditCard class="w-5 h-5 text-blue-600" />
              Payment Method
            </CardTitle>
          </CardHeader>
          <CardContent>
            <div class="space-y-3">
              <button @click="paymentMethod = 'bkash'" :class="[
                'w-full p-4 rounded-lg border-2 flex items-center gap-3 transition-all duration-200',
                paymentMethod === 'bkash'
                  ? 'border-pink-500 bg-pink-50'
                  : 'border-gray-200 hover:border-pink-300'
              ]">
                <div class="w-12 h-12 bg-pink-500 rounded-lg flex items-center justify-center text-white font-bold">
                  bKash
                </div>
                <div class="text-left flex-1">
                  <p class="font-semibold text-gray-900">bKash</p>
                  <p class="text-sm text-gray-600">Pay with bKash mobile banking</p>
                </div>
                <div v-if="paymentMethod === 'bkash'" class="text-pink-500">
                  ✓
                </div>
              </button>

              <button @click="paymentMethod = 'nagad'" :class="[
                'w-full p-4 rounded-lg border-2 flex items-center gap-3 transition-all duration-200',
                paymentMethod === 'nagad'
                  ? 'border-orange-500 bg-orange-50'
                  : 'border-gray-200 hover:border-orange-300'
              ]">
                <div class="w-12 h-12 bg-orange-500 rounded-lg flex items-center justify-center text-white font-bold">
                  Nagad
                </div>
                <div class="text-left flex-1">
                  <p class="font-semibold text-gray-900">Nagad</p>
                  <p class="text-sm text-gray-600">Pay with Nagad mobile banking</p>
                </div>
                <div v-if="paymentMethod === 'nagad'" class="text-orange-500">
                  ✓
                </div>
              </button>

              <button @click="paymentMethod = 'card'" :class="[
                'w-full p-4 rounded-lg border-2 flex items-center gap-3 transition-all duration-200',
                paymentMethod === 'card'
                  ? 'border-blue-500 bg-blue-50'
                  : 'border-gray-200 hover:border-blue-300'
              ]">
                <div class="w-12 h-12 bg-blue-500 rounded-lg flex items-center justify-center">
                  <CreditCard class="w-6 h-6 text-white" />
                </div>
                <div class="text-left flex-1">
                  <p class="font-semibold text-gray-900">Credit/Debit Card</p>
                  <p class="text-sm text-gray-600">Pay with Visa, Mastercard, or AMEX</p>
                </div>
                <div v-if="paymentMethod === 'card'" class="text-blue-500">
                  ✓
                </div>
              </button>
            </div>
          </CardContent>
        </Card>
      </div>

      <!-- Order Summary - Right Side -->
      <div class="lg:col-span-1">
        <Card class="sticky top-4">
          <CardHeader>
            <CardTitle class="text-xl flex items-center gap-2">
              <ShoppingBag class="w-5 h-5 text-blue-600" />
              Order Summary
            </CardTitle>
          </CardHeader>
          <CardContent class="space-y-4">
            <!-- Service Details -->
            <div class="pb-4 border-b">
              <div class="flex items-start gap-2 mb-2">
                <Wrench class="w-5 h-5 text-blue-600 mt-0.5" />
                <div>
                  <p class="font-semibold text-gray-900">{{ bookingDetails.serviceName }}</p>
                  <p class="text-sm text-gray-600">{{ bookingDetails.serviceCenter }}</p>
                </div>
              </div>
              <div class="flex items-center gap-2 text-sm text-gray-600 mt-3">
                <Calendar class="w-4 h-4" />
                <span>{{ bookingDetails.date }}</span>
              </div>
              <div class="flex items-center gap-2 text-sm text-gray-600 mt-1">
                <Clock class="w-4 h-4" />
                <span>{{ bookingDetails.time }}</span>
              </div>
            </div>

            <!-- Price Breakdown -->
            <div class="space-y-3">
              <div class="flex justify-between text-gray-600">
                <span>Service Price</span>
                <span>৳{{ bookingDetails.price.toLocaleString() }}</span>
              </div>
              <div class="flex justify-between text-gray-600">
                <span>Booking Fee</span>
                <span>৳{{ bookingDetails.bookingFee.toLocaleString() }}</span>
              </div>
              <div class="pt-3 border-t flex justify-between items-center">
                <span class="font-semibold text-gray-900">Pay Now</span>
                <span class="text-2xl font-bold text-blue-600">৳{{ bookingDetails.bookingFee }}</span>
              </div>
              <div class="text-xs text-gray-500 bg-gray-50 p-3 rounded-lg">
                Remaining ৳{{ (bookingDetails.price - bookingDetails.bookingFee).toLocaleString() }} will be paid at the
                service center
              </div>
            </div>

            <!-- Payment Button -->
            <Button @click="processPayment" class="w-full py-6 text-lg h-auto" :disabled="processing">
              <span v-if="processing">Processing...</span>
              <span v-else>Pay ৳{{ bookingDetails.bookingFee }}</span>
            </Button>

            <!-- Security Note -->
            <div class="text-xs text-center text-gray-500 pt-2">
              🔒 Secure payment powered by SSL encryption
            </div>
          </CardContent>
        </Card>
      </div>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-family: 'Telenor', sans-serif;
}
</style>
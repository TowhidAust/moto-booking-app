<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { Home, Wrench, MapPin, User } from 'lucide-vue-next'
</script>

<template>
  <div class="bg-gray-50 relative pb-20">
    <RouterView />
    
    <!-- Bottom Mobile Navigation -->
    <nav class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200 shadow-lg z-50">
      <div class="flex items-center justify-around max-w-7xl mx-auto">
        <RouterLink 
          to="/" 
          class="flex flex-col items-center justify-center py-3 px-4 text-gray-600 hover:text-blue-600 transition-colors flex-1"
          active-class="text-blue-600"
        >
          <Home class="w-6 h-6 mb-1" />
          <span class="text-xs font-medium">Home</span>
        </RouterLink>

        <RouterLink 
          to="/service-centers" 
          class="flex flex-col items-center justify-center py-3 px-4 text-gray-600 hover:text-blue-600 transition-colors flex-1"
          active-class="text-blue-600"
        >
          <MapPin class="w-6 h-6 mb-1" />
          <span class="text-xs font-medium">Centers</span>
        </RouterLink>

        <RouterLink 
          to="/doorstep-service" 
          class="flex flex-col items-center justify-center py-3 px-4 text-gray-600 hover:text-blue-600 transition-colors flex-1"
          active-class="text-blue-600"
        >
          <Wrench class="w-6 h-6 mb-1" />
          <span class="text-xs font-medium">Doorstep</span>
        </RouterLink>

        <RouterLink 
          to="/profile" 
          class="flex flex-col items-center justify-center py-3 px-4 text-gray-600 hover:text-blue-600 transition-colors flex-1"
          active-class="text-blue-600"
        >
          <User class="w-6 h-6 mb-1" />
          <span class="text-xs font-medium">Profile</span>
        </RouterLink>
      </div>
    </nav>
  </div>
</template>

<style scoped>
nav a.router-link-active {
  color: #2563eb;
}
</style>

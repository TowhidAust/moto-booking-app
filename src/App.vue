<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="bg-gray-50 relative">
    <header class="sticky top-0 z-10">
      <div class="wrapper">
        <nav class="flex gap-4 p-4 bg-black text-white">
          <div class="flex-1 flex gap-4">
            <RouterLink to="/">Home</RouterLink>
            <RouterLink to="/service-centers">Service Centers</RouterLink>
            <RouterLink to="/doorstep-servicing">Doorstep Servicing</RouterLink>
          </div>

          <div class="flex gap-4">
            <RouterLink to="/login">Login</RouterLink>
            <RouterLink to="/profile">Profile</RouterLink>
          </div>
        </nav>
      </div>
    </header>
    <RouterView />
  </div>
</template>

<style scoped></style>

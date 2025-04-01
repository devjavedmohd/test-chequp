<template>
  <header class="bg-white text-gray-600 border-b border-gray-300 shadow-sm h-[68px] flex items-center">
    <nav class="container mx-auto px-6">
      <div class="flex items-center justify-between">
        <div class="text-xl font-bold bg-orange-600 p-2 rounded-xl">
          <RouterLink to="/" class="text-black hover:text-gray-900 ">
            <img :src="logo" alt="Chequp Logo" class="h-6">
          </RouterLink>
        </div>
        <div class="space-x-4 text-sm">
          <RouterLink to="/" class="hover:text-gray-900">Home</RouterLink>
          <RouterLink to="/about" class="hover:text-gray-900">About</RouterLink>
          <RouterLink to="/contact" class="hover:text-gray-900">Contact</RouterLink>
          <RouterLink to="/contact" class="hover:text-gray-900">Get Started</RouterLink>
        </div>
      </div>
    </nav>
  </header>
</template>

<script setup lang="ts">
import logo from '../assets/logo.png';

import { RouterLink } from 'vue-router';
</script>

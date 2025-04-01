<template>
  <div class="flex flex-col items-center text-center px-6 py-8 bg-zinc-100 rounded-lg">
    <h1 class="text-3xl font-bold text-gray-800">Welcome to Our Service</h1>
    <p class="text-gray-600 mt-3">Please add items to your cart to begin</p>
    <button @click="$emit('complete')"
      class="mt-4 px-6 py-2 bg-orange-600 text-white font-semibold rounded-xl hover:bg-orange-600 transition">
      Proceed to Checkout
    </button>
  </div>
</template>

<script setup lang="ts">
defineEmits<{
  (event: 'complete'): void
}>()
</script>
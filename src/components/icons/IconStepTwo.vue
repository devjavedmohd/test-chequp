<template>
  <svg xmlns="http://www.w3.org/2000/svg" :width="size" :height="size" viewBox="0 0 36 36" fill="none">
    <circle cx="17.7729" cy="18.3452" r="17" :stroke="strokeColor" />
    <circle cx="17.7729" cy="18.3452" r="12.5782" :fill="fillColor" />
    <path
      d="M19.1742 12.0397V14.8421C19.1742 15.028 19.248 15.2062 19.3794 15.3375C19.5108 15.4689 19.689 15.5428 19.8748 15.5428H22.6773M19.1742 12.0397H14.2699C13.8983 12.0397 13.5418 12.1873 13.2791 12.4501C13.0163 12.7129 12.8687 13.0693 12.8687 13.4409V23.2495C12.8687 23.6212 13.0163 23.9776 13.2791 24.2403C13.5418 24.5031 13.8983 24.6508 14.2699 24.6508H21.276C21.6477 24.6508 22.0041 24.5031 22.2669 24.2403C22.5296 23.9776 22.6773 23.6212 22.6773 23.2495V15.5428M19.1742 12.0397L22.6773 15.5428M15.6711 21.8483H19.8748M15.6711 19.0458H19.8748"
      stroke="white" stroke-linecap="round" stroke-linejoin="round" />
  </svg>
</template>
<script setup>
defineProps({
  strokeColor: String,
  fillColor: String,
  size: Number
})
</script>
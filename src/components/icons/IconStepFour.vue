<template>
  <svg xmlns="http://www.w3.org/2000/svg" :width="size" :height="size" viewBox="0 0 36 36" fill="none">
    <circle cx="17.7729" cy="18.3452" r="17" :stroke="strokeColor" />
    <circle cx="17.7729" cy="18.3452" r="12.5782" :fill="fillColor" />
    <path d="M23.7731 14.9702L17.7731 11.5952L11.7731 14.9702M23.7731 14.9702V21.7202L17.7731 25.0952M23.7731 14.9702L17.7731 18.3452M17.7731 25.0952L11.7731 21.7202V14.9702M17.7731 25.0952V18.3452M11.7731 14.9702L17.7731 18.3452M14.923 16.6954L20.623 13.2454" stroke="white" stroke-linecap="round" stroke-linejoin="round"/>
  </svg>
</template>
<script setup>
defineProps({
  strokeColor: String,
  fillColor: String,
  size: Number
})
</script>
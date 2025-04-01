<template>
  <div v-if="show" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50">
    <div class="bg-white rounded-lg w-11/12 max-w-md overflow-hidden text-center pb-6">
      <div class="flex justify-center py-6">
        <div class="text-green-500">
          <svg xmlns="http://www.w3.org/2000/svg" width="53" height="53" viewBox="0 0 53 53" fill="none">
            <circle cx="26.2729" cy="26.2305" r="25.481" stroke="#A2DBDF" stroke-width="1.49888" />
            <circle cx="26.2732" cy="26.2305" r="18.8533" fill="#087B8C" />
            <path
              d="M15.4479 25.9657L23.3776 36.6948C23.9763 37.5051 25.1948 37.4349 25.6997 36.5614L37.1585 16.7258C37.7552 15.6928 36.3938 14.6543 35.582 15.5238L23.6439 28.3114L16.7171 24.4774C15.7809 23.9594 14.8081 25.0997 15.4479 25.9657Z"
              fill="white" />
          </svg>
        </div>
      </div>
      <h2 class="text-center text-xl font-semibold pt-2">{{ title }}</h2>
      <p class="text-center text-gray-700 px-4 pt-2 pb-4">{{ message }}</p>
      <button class="w-40 py-2 bg-orange-500 text-white font-semibold rounded-lg hover:bg-orange-600 transition-colors"
        @click="onConfirm">
        {{ buttonText }}
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Props {
  show: boolean
  title: string
  message: string
  buttonText: string
}

interface Emits {
  (event: 'confirm'): void
  (event: 'update:show', value: boolean): void
}

const props = defineProps<Props>()
const emit = defineEmits<Emits>()

const onConfirm = () => {
  emit('confirm')
  emit('update:show', false)
}
</script>

<template>
  <div v-if="show" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50">
    <div class="bg-white rounded-lg w-11/12 max-w-md shadow-lg overflow-hidden">
      <div class="flex justify-between items-center p-4 border-b">
        <h3 class="text-md text-gray-800 font-semibold">Upload a {{ title }} photo of your {{ documentType }}</h3>
        <button class="text-2xl text-white rounded-lg bg-orange-500 hover:bg-orange-600" @click="onClose">
          <IconClose class="h-8 w-8 p-1" />
        </button>
      </div>
      <div class="p-4">
        <p class="text-sm text-center mb-6">Regulations require you to upload a driving licence. <br /> Don't worry,
          your data will stay safe and private</p>
        <div class="flex flex-col justify-around mb-6" v-if="!previewImage">
          <div
            class="flex flex-col w-full h-48 items-center justify-center p-4 border-2 border-dashed border-gray-300 rounded-lg cursor-pointer hover:border-blue-500 hover:bg-blue-50 transition"
            @click="triggerFileInput">
            <IconImg :icon-color="`#15803d`" class="h-8 w-8 mr-3 text-green-700" />
            <span class="mt-2 text-sm text-gray-700 font-bold">Drag & Drop or <span class="text-orange-500">choose</span> file to upload</span>
            <span class="mt-2 text-sm text-gray-600">Please select PNG, JPEG, PDF.</span>
            <input type="file" ref="fileInput" @change="handleFileUpload" accept="image/*" hidden />
          </div>

          <div
            class="flex flex-col items-center p-2 mt-6 rounded-lg cursor-pointer bg-orange-500  hover:bg-orange-600 transition"
            @click="openCamera">
            <span class="flex items-center text-md text-white">
              <IconCamera class="h-8 w-8 mr-3" />
              <span class="leading-tight">Open camera & take photo</span>
            </span>
          </div>
        </div>

        <div v-if="previewImage" class="text-center flex justify-center mb-6">
          <img :src="previewImage" alt="Preview" class="max-w-full max-h-60 rounded-md" />
        </div>

        <div class="flex justify-center gap-4 pt-6 border-t border-gray-200">
          <button @click="cancelPreview"
            class="px-8 py-2 bg-white border border-gray-300 text-gray-800 rounded-lg hover:bg-gray-400 transition">Cancel</button>
          <button @click="confirmUpload"
            class="px-8 py-2 bg-orange-500 text-white rounded-lg hover:bg-orange-600 transition"
            :disabled="!previewImage">Confirm</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'


import IconCamera from '../icons/IconCamera.vue'
import IconClose from '../icons/IconClose.vue'
import IconImg from '../icons/IconImg.vue'


interface Props {
  show: boolean
  title: string
  documentType: string
}

interface Emits {
  (event: 'update:show', value: boolean): void
  (event: 'confirm', image: string): void
}

const props = defineProps<Props>()
const emit = defineEmits<Emits>()

const fileInput = ref<HTMLInputElement | null>(null)
const previewImage = ref<string | null>(null)
const tempImageFile = ref<File | null>(null)

const onClose = () => {
  emit('update:show', false)
  previewImage.value = null
  tempImageFile.value = null
}

const triggerFileInput = () => {
  fileInput.value?.click()
}

const handleFileUpload = (event: Event) => {
  const input = event.target as HTMLInputElement
  const file = input.files?.[0]

  if (file && file.type.match('image.*')) {
    const reader = new FileReader()
    reader.onload = (e) => {
      previewImage.value = e.target?.result as string
      tempImageFile.value = file
    }
    reader.readAsDataURL(file)
  }
}

const cancelPreview = () => {
  emit('update:show', false)
  previewImage.value = null
  tempImageFile.value = null
  if (fileInput.value) fileInput.value.value = ''
}

const confirmUpload = () => {
  if (previewImage.value) {
    emit('confirm', previewImage.value)
    onClose()
  }
}

const openCamera = async () => {
  try {
    const stream = await navigator.mediaDevices.getUserMedia({
      video: { facingMode: 'environment', width: { ideal: 1280 }, height: { ideal: 720 } },
      audio: false
    })
    console.log('Camera accessed:', stream)
  } catch (err) {
    console.error('Camera error:', err)
    alert('Could not access camera. Please check permissions.')
  }
}
</script>
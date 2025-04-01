<template>
  <div class="space-y-6">
    <div class="flex flex-col items-center text-center mb-8">
      <div class="flex items-center space-x-3 mb-4">
        <IconSuccess class="w-8" />
        <h1 class="text-3xl font-semibold">Thank You For Your Purchase</h1>
      </div>
      <p class="text-fuchsia-800 border rounded-xl px-8 py-2 leading-tight text-sm">Your Order Number is:
        <span class="font-bold">{{ orderNumber }}</span>
      </p>
    </div>

    <div class="space-y-6 px-6 py-8 bg-zinc-100 rounded-lg">
      <div class="flex flex-col items-center text-center mb-8">
        <h2 class="text-3xl font-semibold mb-4">ID Verification</h2>
        <p class="text-gray-600 text-sm flex flex-col items-center">
          <span>Please Upload A Valid Government-Issued ID To Verify Your Identity.</span>
          <span>This is Required For Processing Your Order Securely.</span>
        </p>
      </div>

      <div class="space-y-5">
        <div class="space-y-1">
          <label for="document-type" class="block text-sm font-semibold text-fuchsia-800">Document*</label>
          <div class="relative">
            <select id="document-type" v-model="documentType"
              class="w-full p-2 pr-10 border rounded-lg text-md appearance-none" required>
              <option value="Driving Licence">Driving Licence</option>
              <option value="Passport">Passport</option>
              <option value="National ID">National ID</option>
            </select>
            <IconDownArrow />
          </div>
        </div>


        <div class="space-y-1">
          <label for="id-number" class="block text-sm font-semibold text-fuchsia-800">ID Number*</label>
          <input id="id-number" v-model="idNumber" type="text" class="w-full p-2 border rounded-lg text-md"
            placeholder="12345664523423" required />
        </div>
      </div>

      <div class="flex gap-5 mb-6">
        <div class="flex-1 space-y-4">
          <h3 class="text-sm font-semibold text-grey-800">Front Side</h3>
          <div
            class="border-2 border-dashed border-gray-300 rounded-lg h-48 flex items-center justify-center cursor-pointer relative overflow-hidden bg-white hover:border-blue-400"
            @click="openUploadModal('front')">
            <div v-if="!frontImage" class="text-center text-gray-500 py-8">
              <span class="flex items-center text-sm">
                <IconImg class="mr-2" /> Upload front ID
              </span>
            </div>
            <div v-else class="w-full h-full relative">
              <img :src="frontImage" alt="Front ID preview" class="w-full h-full object-contain" />
              <div
                class="absolute bottom-0 left-0 right-0 bg-black bg-opacity-60 text-white py-2 px-4 flex justify-between items-center">
                <span class="text-sm font-medium">ID CARD</span>
                <button
                  class="bg-white bg-opacity-20 text-white text-xs py-1 px-3 rounded-sm transition duration-200 hover:bg-opacity-30"
                  @click.stop="openUploadModal('front')">
                  Replace
                </button>
              </div>
            </div>
          </div>
        </div>

        <div class="flex-1 space-y-4">
          <h3 class="text-sm font-semibold text-grey-800">Back Side</h3>
          <div
            class="border-2 border-dashed border-gray-300 rounded-lg h-48 flex items-center justify-center cursor-pointer relative overflow-hidden bg-white hover:border-blue-400"
            @click="openUploadModal('back')">
            <div v-if="!backImage" class="text-center text-gray-500 py-8">
              <span class="flex items-center text-sm">
                <IconImg class="mr-2" /> Upload Back ID
              </span>
            </div>
            <div v-else class="w-full h-full relative">
              <img :src="backImage" alt="Back ID preview" class="w-full h-full object-contain" />
              <div
                class="absolute bottom-0 left-0 right-0 bg-black bg-opacity-60 text-white py-2 px-4 flex justify-between items-center">
                <span class="text-sm font-medium">ID CARD</span>
                <button
                  class="bg-white bg-opacity-20 text-white text-xs py-1 px-3 rounded-sm transition duration-200 hover:bg-opacity-30"
                  @click.stop="openUploadModal('back')">
                  Replace
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="flex gap-8 justify-center">
      <button @click="$emit('cancel')"
        class="px-8 py-3 bg-white border text-gray-600 rounded-lg text-sm leading-tight">Cancel</button>
      <button @click="handleSubmit"
        class="px-8 py-3 bg-orange-500 text-white rounded-lg leading-tight disabled:bg-orange-300"
        :disabled="!isFormValid">
        Submit
      </button>
    </div>

    <UploadModal v-model:show="showUploadModal" :title="currentUploadSide === 'front' ? 'Front' : 'Back'"
      :document-type="documentType" @confirm="handleUploadConfirm" />

    <SuccessModal v-model:show="showSuccessModal" title="ID Verification Successful"
      message="Your ID has been successfully verified." button-text="Continue" @confirm="$emit('complete')" />

  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';

// Icons
import IconDownArrow from '../icons/IconDownArrow.vue';
import IconImg from '../icons/IconImg.vue';
import IconSuccess from '../icons/IconSuccess.vue';
// Modals
import SuccessModal from '../modals/SuccessModal.vue';
import UploadModal from '../modals/UploadModal.vue';

// Props and Emits
interface Props {
  orderNumber: string
}

interface Emits {
  (event: 'cancel'): void
  (event: 'complete'): void
}

const props = defineProps<Props>()
const emit = defineEmits<Emits>()

const documentType = ref('Driving Licence')
const idNumber = ref('')
const frontImage = ref<string | null>(null)
const backImage = ref<string | null>(null)
const showUploadModal = ref(false)
const showSuccessModal = ref(false)
const currentUploadSide = ref<'front' | 'back'>('front')

const isFormValid = computed(() => {
  return documentType.value && idNumber.value && frontImage.value && backImage.value
})

const openUploadModal = (side: 'front' | 'back') => {
  currentUploadSide.value = side
  showUploadModal.value = true
}

const handleUploadConfirm = (image: string) => {
  if (currentUploadSide.value === 'front') {
    frontImage.value = image
  } else {
    backImage.value = image
  }
}

const handleSubmit = () => {
  if (isFormValid.value) {
    showSuccessModal.value = true
  }
}
</script>

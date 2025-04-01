<template>
  <div class="space-y-6 border border-gray-200 bg-white rounded-lg p-10">
    <div class="flex flex-col items-center text-center mb-8">
      <div class="flex items-center space-x-3 mb-4">
        <IconSuccess class="w-8" />
        <h1 class="text-3xl font-semibold">Thank You For Your Purchase</h1>
      </div>
      <p class="text-fuchsia-800 border border-blue-800 rounded-xl px-8 py-2 leading-tight text-sm">
        Your Order Number is: <span class="font-bold">{{ orderNumber }}</span>
      </p>
    </div>

    <div class="space-y-6 px-40 py-8 bg-zinc-100 rounded-lg">
      <h2 class="text-3xl font-semibold text-gray-800 text-center">Upload Your Head-To-Toe Picture</h2>
      <p class="text-gray-600 text-xs text-center">
        To safely prescribe your order, UK law requires a quick body picture to verify height & weight.<br />
        This is 100% confidential and ensures your medication is tailored for you.
      </p>

      <div class="flex flex-col md:flex-row items-start justify-center gap-4 border-t border-gray-200 pt-4 pb-6">
        <div class="w-full md:w-3/6 space-y-4 text-center">
          <h3 class="text-base font-medium text-gray-700">Picture Example</h3>
          <div class="flex gap-4 justify-center">
            <div class="w-36 h-48 bg-green-100 rounded-t-lg relative border-1 border-gray-600">
              <img src="../../assets/img-1.jpg" alt="Example" class="w-full h-full object-cover rounded-t-lg" />
              <div class="bg-gray-200 bg-opacity-60 text-green-600 text-xs py-1 text-center rounded-b-md">Good Example
              </div>
            </div>
            <div class="w-36 h-48 bg-red-100 rounded-t-lg relative">
              <img src="../../assets/img-2.png" alt="Example" class="w-full h-full object-cover rounded-t-lg" />
              <div class="bg-gray-200 bg-opacity-60 text-red-600 text-xs py-1 text-center rounded-b-md">
                Too Close Up
              </div>
            </div>
          </div>
        </div>

        <div class="w-full md:w-3/6 space-y-4 text-center">
          <h3 class="text-base font-medium text-gray-700">Upload Your Picture</h3>
          <div @click="openUploadModal"
            class="border-2 border-dashed border-gray-400 rounded-lg h-48 w-full max-w-sm mx-auto flex items-center justify-center cursor-pointer relative hover:border-blue-500">
            <div v-if="!bodyPicture" class="text-center p-2 flex flex-col items-center text-sm text-gray-500">
              <IconImg class="h-8 w-8 text-gray-400" />
              <span class="mt-2 text-sm text-gray-700 font-bold">Drag & Drop or <span
                  class="text-orange-500">choose</span> file to upload</span>
              <span class="mt-2 text-sm text-gray-600">Please select PNG, JPEG, PDF.</span>
            </div>
            <div v-else class="w-full h-full relative">
              <img :src="bodyPicture" alt="Uploaded preview" class="w-full h-full object-contain rounded-lg" />

            </div>
          </div>
          <div v-if="bodyPicture" class="flex items-center justify-around">
            <div
              class="flex items-center cursor-pointer justify-center border border-red-600 text-red-600 text-xs text-center rounded-lg px-2 py-1"
              @click.stop="removeBodyPicture">
              <IconTrash class="h-5 w-5 mr-2" />
              <span class="text-sm">Remove</span>
            </div>

            <div
              class="flex items-center cursor-pointer justify-center border border-green-600 text-green-600 text-xs text-center rounded-lg px-2 py-1"
              @click.stop="confirmBodyPicture">
              <IconConfirm class="h-5 w-5 mr-2" />
              <span class="text-sm">Confirm</span>
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
        :disabled="!bodyPicture || !isConfirmed">
        Submit
      </button>
    </div>
    <UploadModal document-type="" v-model:show="showUploadModal" title="Head-To-Toe Picture"
      @confirm="handleUploadConfirm" />

    <SuccessModal v-model:show="showSuccessModal" title="Upload Successful"
      message="Your head-to-toe picture has been successfully uploaded." button-text="View Order Status"
      @confirm="$emit('complete')" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import IconConfirm from '../icons/IconConfirm.vue';
import IconImg from '../icons/IconImg.vue';
import IconSuccess from '../icons/IconSuccess.vue';
import IconTrash from '../icons/IconTrash.vue';
import SuccessModal from '../modals/SuccessModal.vue';
import UploadModal from '../modals/UploadModal.vue';

interface Props {
  orderNumber: string;
}

interface Emits {
  (event: 'cancel'): void;
  (event: 'complete'): void;
}

const props = defineProps<Props>();
const emit = defineEmits<Emits>();

const isConfirmed = ref(false);
const bodyPicture = ref<string | null>(null);
const showUploadModal = ref(false);
const showSuccessModal = ref(false);

const confirmBodyPicture = () => {
  if (bodyPicture.value) {
    isConfirmed.value = true;
  }
};

const handleSubmit = () => {
  if (bodyPicture.value && isConfirmed.value) {
    showSuccessModal.value = true;
  }
};

const openUploadModal = () => {
  showUploadModal.value = true;
};

const handleUploadConfirm = (image: string) => {
  bodyPicture.value = image;
};

const removeBodyPicture = () => {
  bodyPicture.value = null;
  isConfirmed.value = false;
};
</script>

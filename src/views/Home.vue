<template>
  <div class="container mx-auto px-6 py-8">
    <div class="mx-auto p-6 font-sans text-gray-800">
      <ProgressTracker class="max-w-3xl mx-auto" :current-step="currentStep" :steps="steps" />

      <AddToCart class="max-w-3xl mx-auto" v-if="currentStep === 1" @complete="completeStep1" />

      <IdVerification class="max-w-3xl mx-auto" v-if="currentStep === 2" :order-number="orderNumber"
        @cancel="cancelStep2" @complete="completeStep2" />

      <PictureUpload class="md:container max-w-3xl mx-auto" v-if="currentStep === 3" :order-number="orderNumber"
        @cancel="cancelStep3" @complete="completeStep3" />

      <div v-if="currentStep === 4" class="step-container bg-white rounded-lg p-8 mt-6">
        <div class="max-w-3xl mx-auto px-40 flex justify-center flex-col items-center">
          <IconOrderComplete class="w-16 h-16 text-green-500 mb-4" />
          <h1 class="text-center text-2xl text-gray-800 mb-2 font-bold">
            Order Successfully Complete!</h1>
          <p class="text-center">Thank you for completing all the required steps. <br /> Your order has been processed
            and will be prepared
            according to your verified information.</p>
        </div>

        <div class="max-w-md mx-auto flex flex-col items-center justify-center mt-6 bg-gray-100 px-8 py-4 rounded-lg">
          <div class="flex pb-3 w-full border-b border-gray-300 mb-3 justify-center">
            <IconBox class="w-6 h-6 mr-2" />
            <span class="text-md">Order Details</span>
          </div>
          <div class="flex mb-3">
            <IconSuccess class="w-6 h-6 mr-2" />
            <span class="text-md">ID Verification Compete</span>
          </div>
          <div class="flex mb-3">
            <IconSuccess class="w-6 h-6 mr-2" />
            <span class="text-md">Physical Assessment Uploaded</span>
          </div>
          <div class="flex mb-3">
            <IconSuccess class="w-6 h-6 mr-2" />
            <span class="text-md">Prescription Review In Progress</span>
          </div>
        </div>
        <!-- <div>Start new order</div> -->
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref } from 'vue'
import IconBox from '../components/icons/IconBox.vue'
import IconOrderComplete from '../components/icons/IconOrderComplete.vue'
import IconSuccess from '../components/icons/IconSuccess.vue'
import ProgressTracker from '../components/ProgressTracker.vue'
import AddToCart from '../components/steps/AddToCart.vue'
import IdVerification from '../components/steps/IdVerification.vue'
import PictureUpload from '../components/steps/PictureUpload.vue'

const currentStep = ref(1)
const orderNumber = ref('CHEQ-5763')

const steps = reactive([
  { number: 1, title: 'Add To Cart', completed: false },
  { number: 2, title: 'ID Verification', completed: false },
  { number: 3, title: 'Upload Picture', completed: false },
  { number: 4, title: 'Order Complete', completed: false }
])

const completeStep1 = () => {
  steps[0].completed = true
  currentStep.value = 2
}

const cancelStep2 = () => {
  currentStep.value = 1
}

const completeStep2 = () => {
  steps[1].completed = true
  currentStep.value = 3
}

const cancelStep3 = () => {
  currentStep.value = 2
}

const completeStep3 = () => {
  steps[2].completed = true
  steps[3].completed = true
  currentStep.value = 4
}
</script>

<template>
  <div class="flex justify-between mb-10 relative">
    <div v-for="step in steps" :key="step.number" class="flex flex-col relative z-10 flex-1 items-start">
      <div v-if="step.number !== 4 && step.number < steps.length"
        class="progress-bar absolute top-4 h-0.5 z-0" :class="{
          'bg-cyan-600': currentStep >= step.number || step.completed,
          'bg-gray-300': currentStep < step.number && !step.completed
        }"></div>

      <div class="w-8 h-8 rounded-full flex items-center justify-center font-bold mb-2">
        <component :is="getIconForStep(step.number)" :stroke-color="getIconColor(step).strokeColor"
          :fill-color="getIconColor(step).fillColor" :size="getIconColor(step).size" />
      </div>

      <div class="text-left">
        <div class="text-sm">Step {{ step.number }}</div>
        <div class="font-bold text-sm">{{ step.title }}</div>
        <div class="text-xs" :class="{
          'text-cyan-600': currentStep >= step.number || step.completed,
          'text-gray-500': currentStep < step.number && !step.completed
        }">
          <div>{{ getStepStatus(step) }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import IconStepFour from '../components/icons/IconStepFour.vue';
import IconStepOne from '../components/icons/IconStepOne.vue';
import IconStepThree from '../components/icons/IconStepThree.vue';
import IconStepTwo from '../components/icons/IconStepTwo.vue';

interface Step {
  number: number
  title: string
  completed: boolean
}

interface Props {
  currentStep: number
  steps: Step[]
}

const props = defineProps<Props>()

const getStepStatus = (step: Step) => {
  if (step.completed) return "Completed"
  if (props.currentStep === step.number) return "In Progress"
  return "Pending"
}

// Method to return the correct icon based on step number
const getIconForStep = (stepNumber: number) => {
  switch (stepNumber) {
    case 1:
      return IconStepOne
    case 2:
      return IconStepTwo
    case 3:
      return IconStepThree
    case 4:
      return IconStepFour
    default:
      return IconStepOne // default icon
  }
}

const getIconColor = (step: Step) => {
  return {
    strokeColor: step.completed
      ? '#0891b2'
      : (step.number === props.currentStep ? '#0891b2' : '#E7E7E6'), // Active step gets blue
    fillColor: step.completed
      ? '#0891b2'
      : (step.number === props.currentStep ? '#0891b2' : '#18191C'), // Active step gets light blue
    size:36
  }
}

</script>

<style scoped>
.progress-bar {
  width: calc(100% - 52px);
  left: 42px;
  height: 3px;
  border-radius: 2px;
}
</style>
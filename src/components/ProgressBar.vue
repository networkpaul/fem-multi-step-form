<template>
  <div class="progressBar">
    <div class="progressBar-steps">
      <ProgressBarStep
          v-for="step in steps"
          :key="step.number"
          :step-number="step.number"
          :current-step="currentStep"
          :step-text="step.text">
      </ProgressBarStep>
    </div>
    <img class="progressBar-background" src="@/images/bg-sidebar-desktop.svg" alt="progressBar-background">
  </div>
</template>

<script>
import ProgressBarStep from "@/components/ProgressBarStep.vue";

export default {
  name: 'ProgressBar',
  components: {ProgressBarStep},

  props: {
    currentStep: {
      type: Number,
      default: 1
    }
  },

  data() {
    return {
      steps: [
        {
          number: 1,
          text: "YOUR INFO",
        },
        {
          number: 2,
          text: "SELECT PLAN",
        },
        {
          number: 3,
          text: "ADD-ONS",
        },
        {
          number: 4,
          text: "SUMMARY",
        },
      ]
    }
  },
}
</script>

<template>
  <div class="multiStepForm">
    <ProgressBar :current-step="currentStep" />
    <StepOne v-if="currentStep === 1" @next-step="handleStepData" />
    <StepTwo v-else-if="currentStep === 2" @next-step="handleStepData" @previous-step="previousStep" />
    <StepThree v-else-if="currentStep === 3" @next-step="handleStepData" @previous-step="previousStep" :form-infos="formInfos" />
    <StepFour v-else-if="currentStep === 4" @next-step="handleStepData" @previous-step="previousStep" @change-plan="changePlan" :form-infos="formInfos" />
    <StepFive v-else-if="currentStep === 5" />
  </div>
  <pre>{{ formInfos }}</pre>
</template>

<script>
import ProgressBar from "./ProgressBar.vue";
import StepOne from "./StepOne.vue";
import StepTwo from "./StepTwo.vue";
import StepThree from "./StepThree.vue";
import StepFour from "./StepFour.vue";
import StepFive from "./StepFive.vue";

export default {
  name: 'MultiStepForm',
  components: {StepFive, StepFour, StepThree, StepTwo, StepOne, ProgressBar},
  data() {
    return {
      currentStep: 1,
      formInfos: {}
    }
  },

  methods: {
    previousStep() {
      this.currentStep -= 1
    },

    changePlan() {
      this.currentStep = 2
    },

    handleStepData(data) {
      this.formInfos = { ...this.formInfos, ...data }

      this.$nextTick(() => {
        this.currentStep += 1
      })
    },
  }
}
</script>

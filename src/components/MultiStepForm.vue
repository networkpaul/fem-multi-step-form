<template>
  <div class="multiStepForm">
    <ProgressBar />
    <StepOne
        v-if="stepOne"
        class="multiStepForm-step"
        @all-fields-filled="buttonNextStepDisabled = false"
        @no-fields-filled="buttonNextStepDisabled = true"
    >
      <template #buttonNextStep>
        <button
            :class="{ 'c2a--disabled': buttonNextStepDisabled }"
            class="c2a c2a-main"
            :disabled="buttonNextStepDisabled"
            @click="stepOne = false, stepTwo = true"
        >
          Next Step
        </button>
      </template>
    </StepOne>
    <StepTwo
        v-else-if="!stepOne && stepTwo"
        @select-option="buttonNextStepDisabled = false"
    >
      <template #buttonPreviousStep>
        <button
            class="c2a c2a-secondary"
            @click="stepOne = true, stepTwo = false"
        >
          Go Back
        </button>
      </template>
      <template #buttonNextStep>
        <button
            :class="{ 'c2a--disabled': buttonNextStepDisabled }"
            class="c2a c2a-main"
            :disabled="buttonNextStepDisabled"
            @click="stepTwo = false, stepThree = true"
        >
          Next Step
        </button>
      </template>
    </StepTwo>
    <StepThree v-else-if="!stepOne && !stepTwo && stepThree">
      <template #buttonPreviousStep>
        <button
            class="c2a c2a-secondary"
            @click="stepTwo = true, stepThree = false"
        >
          Go Back
        </button>
      </template>
      <template #buttonNextStep>
        <button class="c2a c2a-main">
          Next Step
        </button>
      </template>
    </StepThree>
  </div>
</template>

<script>
import ProgressBar from "./ProgressBar.vue";
import StepOne from "./StepOne.vue";
import StepTwo from "./StepTwo.vue";
import StepThree from "./StepThree.vue";

export default {
  name: 'MultiStepForm',
  components: {StepThree, StepTwo, StepOne, ProgressBar},
  data() {
    return {
      buttonNextStepDisabled: true,
      stepOne: true,
      stepTwo: false,
      stepThree: false
    }
  },

  updated() {
    this.buttonNextStepDisabled = true
  }
}
</script>

<template>
  <div class="multiStepForm-stepTwo">
    <h1 class="multiStepForm-stepTitle">Select your plan</h1>
    <h3 class="multiStepForm-stepSubtitle">You have the option of monthly or yearly billing.</h3>
    <div class="multiStepForm-options">
      <div
          v-for="optionCard in optionCards"
          :key="optionCard.id"
          :class="{ 'multiStepForm-option--selected': selectedCardOption === optionCard }"
          class="multiStepForm-option"
          @click="selectOption(optionCard)"
      >
        <span class="multiStepForm-optionIcon" :class="'multiStepForm-optionIcon--' + optionCard.title.toLowerCase()">
          <i></i>
        </span>
        <span class="multiStepForm-optionTitle">{{ optionCard.title }}</span>
        <span v-if="planType === 'monthly'" class="multiStepForm-optionPrice">{{ optionCard.pricePerMonth }}</span>
        <span v-else class="multiStepForm-optionPrice">{{ optionCard.pricePerYear }}</span>
        <span :class="{ 'multiStepForm-optionFreeMonth--visible' : planType !== 'monthly'}" class="multiStepForm-optionFreeMonth">2 months free</span>
      </div>
    </div>
    <div class="multiStepForm-choices">
      <span
          class="multiStepForm-choice"
          :class="{ 'multiStepForm-choice--selected' : planType === 'monthly' }"
      >
        Monthly
      </span>
      <label class="switch">
        <input type="checkbox" @click="planType = planType === 'monthly' ? 'yearly' : 'monthly'">
        <span class="slider"></span>
      </label>
      <span
          class="multiStepForm-choice"
          :class="{ 'multiStepForm-choice--selected' : planType !== 'monthly' }"
      >
        Yearly
      </span>
    </div>
    <div class="multiStepForm-actions">
      <div class="multiStepForm-previousStep">
        <button class="c2a c2a-secondary" @click="previousStep">
          Go Back
        </button>
      </div>
      <div class="multiStepForm-nextStep">
        <button
            :class="{ 'c2a--disabled': buttonNextStepDisabled }"
            class="c2a c2a-main"
            :disabled="buttonNextStepDisabled"
            @click="nextStep"
        >
          Next Step
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StepTwo',
  data() {
    return {
      currentStep: 2,
      buttonNextStepDisabled: true,
      selectedCardOption: null,
      planType: 'monthly',
      optionCards: [
        {
          id: 1,
          icon: '',
          title: 'Arcade',
          pricePerMonth: '$9/mo',
          pricePerYear: '$90/yr'
        },
        {
          id: 2,
          icon: '',
          title: 'Advanced',
          pricePerMonth: '$12/mo',
          pricePerYear: '$120/yr'
        },
        {
          id: 3,
          icon: '',
          title: 'Pro',
          pricePerMonth: '$15/mo',
          pricePerYear: '$150/yr'
        }
      ],
    }
  },

  computed: {
    allInputsFilled() {
      return !!this.selectedCardOption
    }
  },

  methods: {
    nextStep() {
      this.$emit('next-step', {
        plan: this.selectedCardOption,
        planType: this.planType,
        currentStep: this.currentStep,
      });
    },

    previousStep() {
      this.$emit('previous-step', this.currentStep);
    },

    selectOption(optionCard) {
      this.selectedCardOption = optionCard
    }
  },

  watch: {
    allInputsFilled(value) {
      if (this.allInputsFilled) {
        this.buttonNextStepDisabled = false
      }
    }
  }
}
</script>

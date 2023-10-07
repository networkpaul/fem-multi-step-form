<template>
  <div class="multiStepForm-stepTwo">
    <h1 class="multiStepForm-stepTitle">Select your plan</h1>
    <h3 class="multiStepForm-stepSubtitle">You have the option of monthly or yearly billing.</h3>
    <div class="multiStepForm-options">
      <div
          v-for="optionCard in optionCards"
          :key="optionCard.id"
          :class="{ 'multiStepForm-option--selected': selectedCardOption === optionCard.id }"
          class="multiStepForm-option"
          @click="selectOption(optionCard.id)"
      >
        <span class="multiStepForm-optionIcon" :class="'multiStepForm-optionIcon--' + optionCard.title.toLowerCase()">
          <i></i>
        </span>
        <span class="multiStepForm-optionTitle">{{ optionCard.title }}</span>
        <span v-if="!payMonthly" class="multiStepForm-optionPrice">{{ optionCard.pricePerMonth }}</span>
        <span v-else class="multiStepForm-optionPrice">{{ optionCard.pricePerYear }}</span>
        <span :class="{ 'multiStepForm-optionFreeMonth--visible' : payMonthly}" class="multiStepForm-optionFreeMonth">2 months free</span>
      </div>
    </div>
    <div class="multiStepForm-choices">
      <span
          class="multiStepForm-choice"
          :class="{ 'multiStepForm-choice--selected' : !payMonthly }"
      >
        Monthly
      </span>
      <label class="switch">
        <input type="checkbox" v-model="payMonthly">
        <span class="slider"></span>
      </label>
      <span
          class="multiStepForm-choice"
          :class="{ 'multiStepForm-choice--selected' : payMonthly }"
      >
        Yearly
      </span>
    </div>
    <div v-if="$slots.buttonNextStep || $slots.buttonPreviousStep" class="multiStepForm-actions">
      <div v-if="$slots.buttonPreviousStep" class="multiStepForm-previousStep">
        <slot name="buttonPreviousStep" />
      </div>
      <div v-if="$slots.buttonNextStep" class="multiStepForm-nextStep">
        <slot name="buttonNextStep" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StepTwo',
  data() {
    return {
      selectedCardOption: null,
      payMonthly: true,
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

  methods: {
    selectOption(optionId) {
      this.selectedCardOption = optionId;
      this.$emit('select-option');
    }
  }
}
</script>

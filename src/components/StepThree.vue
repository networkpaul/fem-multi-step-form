<template>
  <div class="multiStepForm-stepThree">
    <h1 class="multiStepForm-stepTitle">Pick add-ons</h1>
    <h3 class="multiStepForm-stepSubtitle">Add-ons help enhance your gaming experience.</h3>
    <div class="multiStepForm-addons">
      <div
          v-for="addonCard in addonCards"
          :key="addonCard.id"
          :class="{ 'multiStepForm-addon--selected': addonCard.checked }"
          class="multiStepForm-addon"
          @click="handleAddonCard(addonCard)"
      >
        <label :for="addonCard.title.toLowerCase().replace(' ', '-')" />
        <input
            type="checkbox"
            :id="addonCard.title.toLowerCase().replace(' ', '-')"
            v-model="addonCard.checked"
        >
        <div class="multiStepForm-addonText">
          <span class="multiStepForm-addonTitle">{{ addonCard.title }}</span>
          <span class="multiStepForm-addonSubtitle">{{ addonCard.subtitle }}</span>
        </div>
        <span v-if="formInfos.planType === 'monthly'" class="multiStepForm-addonPrice">{{ addonCard.pricePerMonth }}</span>
        <span v-else class="multiStepForm-addonPrice">{{ addonCard.pricePerYear }}</span>
      </div>
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
  name: 'StepThree',

  props: {
    formInfos: {
      type: Object,
      default: {}
    }
  },

  data() {
    return {
      currentStep: 3,
      buttonNextStepDisabled: false,
      addonCards: [
        {
          id: 1,
          title: 'Online service',
          subtitle: 'Access to multiplayer games',
          pricePerMonth: '+$1/mo',
          pricePerYear: '+$10/yr',
          checked: false
        },
        {
          id: 2,
          title: 'Larger storage',
          subtitle: 'Extra 1TB of cloud save',
          pricePerMonth: '+$2/mo',
          pricePerYear: '+$20/yr',
          checked: false
        },
        {
          id: 3,
          title: 'Customizable profile',
          subtitle: 'Custom theme on your profile',
          pricePerMonth: '+$2/mo',
          pricePerYear: '+$20/yr',
          checked: false
        },
      ],
      selectedAddons: {}
    }
  },

  methods: {
    nextStep() {
      this.$emit('next-step', {
        addonCards: this.selectedAddons,
        currentStep: this.currentStep
      });
    },

    previousStep() {
      this.$emit('previous-step', this.currentStep);
    },

    handleAddonCard(addonCard) {
      addonCard.checked = !addonCard.checked

      if (addonCard.checked) {
        this.selectedAddons = { ...this.selectedAddons, [addonCard.id]: addonCard }
      } else {
        const updatedAddons = { ...this.selectedAddons }
        delete updatedAddons[addonCard.id]
        this.selectedAddons = updatedAddons
      }
    }
  }
}
</script>

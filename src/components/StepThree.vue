<template>
  <div class="multiStepForm-stepTwo">
    <h1 class="multiStepForm-stepTitle">Pick add-ons</h1>
    <h3 class="multiStepForm-stepSubtitle">Add-ons help enhance your gaming experience.</h3>
    <div class="multiStepForm-addons">
      <div
          v-for="addonCard in addonCards"
          :key="addonCard.id"
          :class="{ 'multiStepForm-addon--selected': addonCard.checked }"
          class="multiStepForm-addon"
          @click="addonCard.checked = !addonCard.checked"
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
        <span v-if="!payMonthly" class="multiStepForm-addonPrice">{{ addonCard.pricePerMonth }}</span>
        <span v-else class="multiStepForm-addonPrice">{{ addonCard.pricePerYear }}</span>
      </div>
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
      payMonthly: true,
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
    }
  }
}
</script>

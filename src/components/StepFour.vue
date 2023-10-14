<template>
  <div class="multiStepForm-stepFour">
    <h1 class="multiStepForm-stepTitle">Finishing up</h1>
    <h3 class="multiStepForm-stepSubtitle">Double-check everything looks OK before confirming.</h3>
    <div class="multiStepForm-recap">
      <p class="multiStepForm-recapItem">
        <span class="multiStepForm-recapItemTitle">{{ formInfos.plan.title }} ({{ formInfos.planType }})</span>
        <span v-if="formInfos.planType === 'monthly'" class="multiStepForm-recapItemPlanPrice">{{ formInfos.plan.pricePerMonth }}</span>
        <span v-else class="multiStepForm-recapItemPrice">{{ formInfos.plan.pricePerYear }}</span>
      </p>
      <button @click="changePlan" class="multiStepForm-changePlan">
        Change
      </button>
      <div class="multiStepForm-recapAddons">
        <span v-for="addon in addonCardArray" :key="addon.id" class="multiStepForm-recapItem">
          <span class="multiStepForm-recapItemTitle">{{ addon.title }}</span>
          <span v-if="formInfos.planType === 'monthly'" class="multiStepForm-recapItemPrice">{{ addon.pricePerMonth }}</span>
          <span v-else class="multiStepForm-recapItemPrice">{{ addon.pricePerYear }}</span>
        </span>
      </div>
      <div class="multiStepForm-recapTotalPrice">
        <span class="multiStepForm-recapItemTitle">Total (per {{ planType }})</span>
        <span class="multiStepForm-recapItemTotalPrice">{{ totalPrice }}</span>
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
            class="c2a c2a-confirm"
            :disabled="buttonNextStepDisabled"
            @click="nextStep"
        >
          Confirm
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StepFour',

  props: {
    formInfos: {
      type: Object,
      default: {}
    }
  },

  data() {
    return {
      currentStep: 4,
      buttonNextStepDisabled: false,
    }
  },

  computed: {
    addonCardArray() {
      return Object.values(this.formInfos.addonCards)
    },

    planType() {
      if (this.formInfos.planType === 'monthly') {
        return 'month'
      } else {
        return 'year'
      }
    },

    totalPrice() {
      let totalPrice = 0

      if (this.formInfos.planType === 'monthly') {
        const planPricePerMonth = parseFloat(this.formInfos.plan.pricePerMonth.replace(/\D/g,''))
        totalPrice += planPricePerMonth

        for (const addon of this.addonCardArray) {
          totalPrice += parseFloat(addon.pricePerMonth.replace(/\D/g,''))
        }

        return '$' + totalPrice + '/mo'
      }

      if (this.formInfos.planType === 'yearly') {
        const planPricePerYear = parseFloat(this.formInfos.plan.pricePerYear.replace(/\D/g,''))
        totalPrice += planPricePerYear

        for (const addon of this.addonCardArray) {
          totalPrice += parseFloat(addon.pricePerYear.replace(/\D/g,''))
        }

        return '$' + totalPrice + '/yr'
      }
    }
  },

  methods: {
    nextStep() {
      this.$emit('next-step', this.currentStep);
    },

    previousStep() {
      this.$emit('previous-step', this.currentStep);
    },

    changePlan() {
      this.$emit('change-plan', this.currentStep);
    }
  }
}
</script>

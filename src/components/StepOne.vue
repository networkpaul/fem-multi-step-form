<template>
  <div class="multiStepForm-stepOne">
    <h1 class="multiStepForm-stepTitle">Personal info</h1>
    <h3 class="multiStepForm-stepSubtitle">Please provide your name, email address, and phone number.</h3>
    <form class="multiStepForm-container">
      <div class="multiStepForm-input">
        <label for="name">Name</label>
        <input v-model="name" id="name" type="text" placeholder="e.g. Stephen King" />
      </div>
      <div class="multiStepForm-input">
        <label for="email">Email Address</label>
        <input v-model="email" id="email" type="email" placeholder="e.g. stephenking@lorem.com" />
      </div>
      <div class="multiStepForm-input">
        <label for="phone">Phone Number</label>
        <input v-model="phone" id="phone" type="tel" placeholder="e.g. +1 234 567 890" />
      </div>
    </form>
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
  name: 'StepOne',
  data() {
    return {
      name: null,
      email: null,
      phone: null,
    }
  },

  computed: {
    allFieldsFilled() {
      if (this.name && this.email && this.phone) {
        return true
      }
    }
  },

  updated() {
    if (this.allFieldsFilled) {
      this.$emit('all-fields-filled')
    }

    if (!this.allFieldsFilled) {
      this.$emit('no-fields-filled')
    }
  }
}
</script>

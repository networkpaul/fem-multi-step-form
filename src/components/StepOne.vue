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
    <div class="multiStepForm-actions">
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
  name: 'StepOne',
  data() {
    return {
      name: null,
      email: null,
      phone: null,
      buttonNextStepDisabled: true,
      currentStep: 1
    }
  },

  computed: {
    allInputsFilled() {
      return !!this.name && !!this.email && !!this.phone
    }
  },

  methods: {
    nextStep() {
      this.$emit('next-step', {
        name: this.name,
        email: this.email,
        phone: this.phone,
        currentStep: this.currentStep,
      });
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

<template>
  <div class="progressBarStep">
    <span class="progressBarStep-number">{{ stepNumber }}</span>
    <div class="progressBarStep-textWrapper">
      <span class="progressBarStep-textNumber">Step {{ stepNumber }}</span>
      <span class="progressBarStep-text">{{ stepText }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProgressBarStep',
  props: {
    stepNumber: {
      type: Number,
      default: null
    },
    stepText: {
      type: String,
      default: null
    }
  }
}
</script>

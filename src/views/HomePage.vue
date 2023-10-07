<template>
  <div class="homePage">
    <MultiStepForm />
  </div>
</template>

<script>


import MultiStepForm from "../components/MultiStepForm.vue";
import StepTwo from "../components/StepTwo.vue";

export default {
  name: 'HomePage',
  components: {StepTwo, MultiStepForm},
}
</script>

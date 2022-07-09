<template>
  <!-- top-step -->
  <div class="step-control">
    <ol class="step-container">
      <li v-for="step in steps" :key="step.id" class="c-stepper__item">
        <div v-show="step.status !== 'checked'" class="step-no" :class="step.status">{{ step.id }}</div>
        <div v-show="step.status === 'checked'" class="step-no" :class="step.status"></div>
        <h3 class="c-stepper__title step-text">{{ step.title }}</h3>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: 'CheckoutFormStepper',
  props: {
    stepNow: {
      type: Number,
      required: true,
    }
  },
  data () {
    return {
      steps: [
        {
          id: 1,
          title: '寄送地址',
          status: 'active',
        },
        {
          id: 2,
          title: '運送方式',
          status: '',
        },
        {
          id: 3,
          title: '付款資訊',
          status: '',
        }
      ],
    }
  },
  watch: {
    stepNow: {
      handler: function () {
        if (this.stepNow === 1) {
          this.steps[0].status = 'active'
          this.steps[1].status = ''
          this.steps[2].status = ''
        }
        if (this.stepNow === 2) {
          this.steps[0].status = 'checked'
          this.steps[1].status = 'active'
          this.steps[2].status = ''
        }
        if (this.stepNow === 3) {
          this.steps[0].status = 'checked'
          this.steps[1].status = 'checked'
          this.steps[2].status = 'active'
        }
      }
    }
  }
}
</script>
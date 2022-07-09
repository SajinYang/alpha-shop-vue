<template>
  <main id="main-container">

    <!-- title -->
    <section class="title">
      <h3>結帳</h3>
    </section>

    <!--------- <left> 資訊欄 ---------->
    <!--------------------------------->

    <div class="section-container">

      <CheckoutForm @form-Info="formInfoNow" />


      <!-------- <right>  購物車 -------->
      <!--------------------------------->
      <CheckoutCar :deliveryFee="formInfo.deliveryFee" />


    </div>


  </main>
</template>

<script>
import CheckoutForm from './../components/CheckoutForm.vue'
import CheckoutCar from './../components/CheckoutCar.vue'

export default {
  components: {
    CheckoutForm,
    CheckoutCar
  },
  data () {
    return {
      formInfo: {
        salutation: '',
        name: '',
        tel: '',
        email: '',
        city: '',
        address: '',
        deliveryFee: 0,
        cardName: '',
        cardNumber: '',
        cardDate: '',
        cardCVC: ''
      }
    }
  },
  methods: {
    formInfoNow(formInfoData) {
      this.formInfo = {
        ...this.formInfo,
        ...formInfoData
      }
    }
  }
}
</script>
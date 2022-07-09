<template>

  <!-- section-left -->
  <section class="left-information">

    <CheckoutFormStepper :stepNow="stepNow" />

    <!-- down-form -->
    <div class="form-panel">
      <div class="form-container">

        <!-- part1.寄送資訊 -->
        <div v-show="stepNow === 1" class="part">
          <h4 class="part-title">寄送地址</h4>
          <div class="form-content part-1">

            <!-- 稱謂下拉式選單 -->
            <div class="form-row salutation">
              <label>稱謂</label>
              <div class="select-wrapper">
                <select v-model="formInfo.salutation" name="a-type" id="a-type" required>
                  <option value="" disabled selected>請選擇稱謂</option>
                  <option value="male">先生</option>
                  <option value="female">小姐</option>
                </select>
              </div>
            </div>

            <!-- 姓名欄位 -->
            <div class="form-row name">
              <label>姓名</label>
              <input v-model="formInfo.name" id="name" type="text" placeholder="請輸入姓名">
            </div>

            <!-- 電話欄位 -->
            <div class="form-row other">
              <label>電話</label>
              <input v-model="formInfo.tel" id="tel" type="text" placeholder="請輸入行動電話">
            </div>

            <!-- email欄位 -->
            <div class="form-row other">
              <label>E-mail</label>
              <input v-model="formInfo.email" id="email" type="text" placeholder="請輸入電子郵件">
            </div>


            <!-- 縣市下拉式選單 -->
            <div class="form-row other">
              <label>縣市</label>
              <div class="select-wrapper">
                <select v-model="formInfo.city" name="a-type" id="a-type" required>
                  <option value="" disabled selected>請選擇縣市</option>
                  <option v-for="city in cities" :key="city.id" :value="city.code">{{ city.name }}</option>
                </select>
              </div>
            </div>

            <!-- 地址欄位 -->
            <div class="form-row other">
              <label>地址</label>
              <input v-model="formInfo.address" id="address" type="text" placeholder="請輸入地址">
            </div>

          </div>
        </div>


        <!-- part 2.運送方式 -->
        <div v-show="stepNow === 2" class="part">
          <h4 class="part-title">運送方式</h4>
          <div class="form-content part-2">

            <div class="delivery-container">
              <!-- normal deliver -->
              <label for="normal" class="form-delivery normal" data-id="1">
                <input v-model="formInfo.deliveryFee" value="0" type="radio" name="shipping" id="normal">
                <span>標準運送</span>
                <span>約3~7個工作天</span>
                <span>免費</span>
              </label>
            </div>


            <div class="delivery-container">
              <!-- DHL deliver -->
              <label for="DHL" class="form-delivery dhl " data-id="2">
                <input v-model="formInfo.deliveryFee" value="500" type="radio" name="shipping" id="DHL">
                <span>DHL 運送</span>
                <span>48小時內送達</span>
                <span>$500</span>
              </label>
            </div>


          </div>
        </div>

        <!-- part 3.付款資訊 -->
        <div v-show="stepNow === 3" class="part">
          <h4 class="part-title">付款資訊</h4>
          <div class="form-content part-3">
            <!-- 持卡人姓名 -->
            <div class="form-row other">
              <label>持卡人姓名</label>
              <input v-model="formInfo.cardName" id="card-name" type="text" placeholder="John Doe">
            </div>

            <!-- 卡號 -->
            <div class="form-row other">
              <label>卡號</label>
              <input v-model="formInfo.cardNumber" id="card-number" type="text" placeholder="1111 2222 3333 4444">
            </div>

            <!-- 有效期限 -->
            <div class="form-row date">
              <label>有效期限</label>
              <input v-model="formInfo.cardDate" id="card-date" type="text" placeholder="MM/YY">
            </div>

            <!-- CVC/CCV -->
            <div class="form-row cvc">
              <label>CVC / CCV</label>
              <input v-model="formInfo.cardCVC" id="card-cvc" type="text" placeholder="123">
            </div>

          </div>
        </div>
      </div>
    </div>

    <!-- form-btn -->
    <div v-show="stepNow === 1" class="form-btn">
      <!-- <button class="btn btn-outline">&larr;上一步</button> -->
      <button class="btn btn-primary" @click.stop.prevent="nextStep">下一步&rarr;</button>
    </div>
    <div v-show="stepNow === 2" class="form-btn">
      <button class="btn btn-outline step-2" @click.stop.prevent="previousStep">&larr;上一步</button>
      <button class="btn btn-primary step-2" @click.stop.prevent="nextStep">下一步&rarr;</button>
    </div>
    <div v-show="stepNow === 3" class="form-btn">
      <button class="btn btn-outline step-2" @click.stop.prevent="previousStep">&larr;上一步</button>
      <button class=" btn btn-primary step-2">確認下單</button>
    </div>

  </section>

</template>

<script>
import CheckoutFormStepper from './CheckoutFormStepper.vue'

export default {
  components: {
    CheckoutFormStepper
  },
  data () {
    return {
      cities: [
        {
          id: 1,
          name: '基隆市',
          code: 'KLU'
        },
        {
          id: 2,
          name: '新北市',
          code: 'TPH'
        },
        {
          id: 3,
          name: '臺北市',
          code: 'TPE'
        },
        {
          id: 4,
          name: '桃園市',
          code: 'TYC'
        },
        {
          id: 5,
          name: '新竹縣',
          code: 'HSH'
        },
      ],
      stepNow: 1,
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
    nextStep () {
      this.stepNow += 1
    },
    previousStep () {
      if (this.stepNow === 1) return
      this.stepNow -= 1
    },
  },
  watch: {
    formInfo: {
      handler: function (formInfoData) {
        this.$emit('form-Info', formInfoData)
      },
      deep: true,
    }
  }
}
</script>
<template>

  <section class="right-cart">
    <div class="car-control">

      <!-- 購物車明細 -->
      <div class="products-container" id="cart-order">

        <div class="cart-title">
          <h4>購物籃</h4>
        </div>

        <!-- 商品 -->
        <div v-for="product in products" :key="product.id" class="cart-item">
          <img :src="product.image" alt="item" class="cart-item_1">
          <span class="product-name">{{ product.name }}</span>
          <div class="product-control">
            <div class="button btn-plus" data-id="1" @click.stop.prevent="addProductQty(product)">＋</div>
            <span class="quantity">{{ product.qty }}</span>
            <div class="button btn-reduce" data-id="1" @click.stop.prevent="reduceProductQty(product)">
              －</div>
          </div>
          <div class="product-subtotal">{{ product.qty * product.price }}</div>
        </div>

        <div class="cart-amount-container">

          <!-- 運費計算欄位 -->
          <div class="count cart-freight">
            <span class="freight-text">運費</span>
            <span class="freight-fee">{{ deliveryFee | deliveryFree }}</span>
          </div>

          <!-- 小計計算欄位 -->
          <div class="count cart-amount">
            <span class="amount-text">小計</span>
            <span class="amount-price">{{ countAmount }}</span>
          </div>

        </div>
      </div>

    </div>
  </section>

</template>

<script>
const dummyData = {
  products: [
  {
    id: '1',
    name: '破壞補丁修身牛仔褲',
    price: 3999,
    image: require('./../assets/image/product_01.jpg'),
    qty: 1,
  },
  {
    id: '2',
    name: '刷色直筒牛仔褲',
    price: 1299,
    image: require('./../assets/image/product_02.jpg'),
    qty: 1
  }
 ]
}

export default {
  props: {
    deliveryFee: {
      type: [Number, String],
      required: true,
      default: 0
    }
  },
  data () {
    return {
      products: [],
      // 原來寫法
      // products: {
      //   id: -1,
      //   name: '',
      //   price: '',
      //   image: '',
      //   qty: '',
        
      // },
      amount: 5298
    }
  },
  created () {
    this.products = dummyData.products
  },
  methods: {
    addProductQty(product) {
      product.qty += 1
      this.amount += product.price
    },
    reduceProductQty(product) { 
      if (product.qty === 0) return
      product.qty -= 1
      this.amount -= product.price
    },
  },
  computed: {
    countAmount() {
      const deliveryFee = Number(this.deliveryFee)
      return this.amount + deliveryFee
    }
  },
  filters: {
    deliveryFree(n) {
      return Number(n) === 0 ? '免費' : '500'
    }    
  }
}
</script>
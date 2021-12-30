<template>
  <section id="recommended-products">
    <h2 class="section-heading">All Products</h2>
    <div class="cards">
      <div  class="cards__item" v-for="product in products" :key="product.id">
        <Product
          :product="product"
          @addToCart="addToCart"
        />
      </div>
    </div>
  </section>
</template>

<script>
import Product from '../components/Product.vue'
export default {
  components : {
    Product,
  },
  props: ['products'],
  methods: {
    addToCart(productId, quantity) {
      this.$emit('addToCart',productId, quantity);
    }
  }
}
</script>

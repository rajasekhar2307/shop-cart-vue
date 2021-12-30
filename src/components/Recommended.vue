<template>
  <section id="recommended-products">
    <h2 class="section-heading">Recommended Products</h2>
    <div class="cards">
      <div  class="cards__item" v-for="product in products" :key="product.id">
        <Product
          :product="product"
          @addToCart="addToCart"
        />
      </div>
    </div>
    <div class="custom-class">
      <router-link class="btn btn-lg btn-orange" to="/products">All Products</router-link>
    </div>
  </section>
</template>

<script>
import Product from './Product.vue'
export default {
  name:"Recommended",
  components: {
    Product
  },
  props: ['products'],
  methods: {
    addToCart(productId, quantity) {
      this.$emit('addToCart',productId, quantity);
    }
  }

}
</script>
<style scoped>
.custom-class {
  display: flex;
  justify-content: center;
  padding: 2rem;
  margin: 2rem;
}
</style>
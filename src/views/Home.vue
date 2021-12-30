<template>
  <div class="home">
    <Banner />
    <Recommended
      @addToCart="addToCart"
      :products="products.slice(0,3)"
    />
  </div>
</template>

<script>
import Banner from '../components/Banner.vue'
import Recommended from '../components/Recommended.vue'

export default {
  name: 'Home',
  components: {
    Banner,
    Recommended
  },
  props: ['products'],
  methods: {
    addToCart(productId, quantity) {
      this.$emit('addToCart',productId, quantity);
    }
  }
}
</script>

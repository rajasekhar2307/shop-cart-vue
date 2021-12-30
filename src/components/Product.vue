<template>
  <div class="product-card">
    <img
      class="card-image"
      :src="product.image"
      alt="Image of MacBook"
    />
    <div class="card-footer">
      <div class="product-title">{{ product.title }}</div>
      <div class="product-description">
        {{ product.description }}
      </div>
    </div>
    <div class="cart-container">
      <h3 class="price">${{ product.price }}</h3>
      <input class="counter" min="0" max="10" type="number" v-model="inventory[product.id]"/>
      <button class="btn btn-sm btn-orange" @click="addToCart(product.id, inventory[product.id])">Add to Cart</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Product',
  props: ['product'],  
  data() {
    return {
      inventory: {
        MBP15 : 0,
        MBA14: 0,
        IP13: 0,
        IP13P: 0,
      },
      cart : {
        MBP15 : 0,
        MBA14: 0,
        IP13: 0,
        IP13P: 0,
      }
    }
  },
  methods: {
    addToCart(productId, quantity) {
      this.$emit('addToCart',productId, quantity);
    }
  }
}
</script>
<template>
  <nav class="navbar">
    <div>
      <router-link class="nav-link" to="/">Home</router-link>
      <router-link class="nav-link" to="/products">Products</router-link>
    </div>
    <div>
      <div class="cart-button nav-link" @click="toggleCart">Cart</div>
    </div>
  </nav>

  <Modal 
    :showCart="showCart"
    :toggleCart="toggleCart"
    :cartItems="cartItems"
    @removeItem='removeItem'
  />

  <router-view :products="products" @addToCart="addToCart"/>
</template>
<script>
import Modal from './components/Modal.vue'

export default {
  name: "App",
  components : {
    Modal,
  },
  data() {
    return {
      showCart: false,
      products: [],
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
      },
      cartItems: [],
    }
  },
  methods : {
    toggleCart() {
      this.showCart = ! this.showCart;
    },
    addToCart(productId, quantity) {
      this.cart[productId] += quantity;

      let product = this.products.filter((p) => {
        return p.id == productId;
      })

      product[0]['quantity'] = this.cart[productId]
      if(!this.cartItems.find((prod) => {
        return prod.id == productId;
      })){
        this.cartItems.push(product[0])
      }
      console.log(this.cartItems)
    },
    removeItem(productId) {
      this.cartItems.forEach((prod, i) => {
        if(prod.id == productId){
          if(this.cart[productId] > 0){
            this.cart[productId] -= 1;
            prod['quantity'] = this.cart[productId]
            if(this.cart[productId] == 0){
              this.cartItems.splice(i, 1)
            }
          }
        }
      });
    }
  },
  async created() {
    const response = await fetch('http://localhost:5500/products');
    const data = await response.json();
    this.products = data;
  }
}
</script>
<style scoped>
.cart-button {
  cursor: pointer;
}
</style>
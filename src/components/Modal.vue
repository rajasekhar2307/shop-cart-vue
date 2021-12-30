<template>
  <section v-if="showCart" class="modal">
    <div class="modal-header">
      <p>Cart</p>
      <p @click="toggleCart">&times;</p>
    </div>
    <table class="modal-content">
      <caption v-if="isEmpty">No Items Available</caption>
      <tr v-if="!isEmpty">
        <th id="item">Item Name</th>
        <th id="up">Unit Price</th>
        <th id="q">Quantity</th>
        <th id="tp">Total Price</th>
        <th id="remove">Remove</th>
      </tr>
      <tr v-for="item in cartItems" :key="item.id">
        <td>{{item.title}}</td>
        <td>${{item.price}}</td>
        <td>{{item.quantity}}</td>
        <td>${{item.quantity * item.price}}</td>
        <td @click="removeItem(item.id)">&times;</td>
      </tr>
      <tr v-if="!isEmpty">
        <td></td>
        <td></td>
        <td>Total</td>
        <td>${{ total }}</td>
        <td></td>
      </tr>
    </table>
    
    <div class="modal-footer">
      <button class="btn btn-sm btn-black" @click="toggleCart">Close</button>
      <button class="btn btn-sm btn-orange">Checkout</button>
    </div>
  </section>
</template>

<script>
export default {
  name: "Modal",
  props: ['showCart', 'toggleCart', 'cartItems'],
  methods: {
    removeItem(productId) {
      this.$emit('removeItem', productId)
    }
  },
  computed: {
    isEmpty() {
      return this.cartItems.length == 0? true:false;
    },
    total() {
      let totalPrice = 0
      this.cartItems.forEach(element => {
        totalPrice += element.quantity * element.price;
      });
      return totalPrice
    }
  }
}
</script>


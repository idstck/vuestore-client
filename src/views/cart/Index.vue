<template>
  <div>
      <div id="page-wrap">
        <h1>Shopping Cart</h1>
        <ItemCart 
          v-for="item in cartItems"
          :key="item.id"

          :item="item"
          v-on:remove-item="removeFromCart($event)"
        />
        <h3 id="total-price">Total: Rp{{ totalPrice }}</h3>
        <button id="checkout-button">Checkout</button>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
// import { cartItems } from '../../data-seed'
import ItemCart from '../../components/ItemCart'

export default {
  components: {
    ItemCart
  },
  data() {
    return {
      cartItems: []
    }
  },
  methods: {
    async removeFromCart(product) {
      await axios.delete(
        `http://localhost:8000/api/orders/delete/user/2/product/${product}`
      )
      let cart = this.cartItems.map(function(item) { 
        return item.code
      }).indexOf(product)
      this.cartItems.splice(cart, 1)
    }
  },
  computed: {
    totalPrice() {
      return this.cartItems.reduce(
        (sum, item) => sum + Number(item.price),
        0
      )
    }
  },
  async created() {
    const result = await axios.get('http://localhost:8000/api/orders/user/2')
    let data = Object.assign({}, 
      ...(result.data.map(
          result => ({ 
            user_id: result.user_id,
            cart_items: result.products, 
          }) 
      ))
    );
    this.cartItems = data.cart_items
  }

}
</script>

<style scoped>
h1 {
    border-bottom: 1px solid #41B883;
    margin: 0;
    margin-top: 16px;
    padding: 16px;
  }
  #total-price {
    padding: 16px;
    text-align: right;
  }
  #checkout-button {
    width: 100%;
  }
</style>
<template>
  <div>
    <h2>Your Cart</h2>
    <hr>
    <div v-for="product in getCart" :key="product._id">
      <h2>{{product.title}}</h2>
      <h3>Qty: {{product.quantity}}</h3>
      <h3>$ {{product.price * product.quantity}}</h3>
      <!-- <div>{{product.rating}}</div> -->
       <img :src="'http://localhost:5000/'+ product.photo"/>
        Qty:
       <select @change="onChangeQuantity($event, product)">
         <option v-for="i in 10" :key="i" :value="i" :selected="checkQty(product.quantity, i)">
           &nbsp;{{i}}
         </option>
       </select>
      <button @click="$store.commit('removeProduct', product)">Remove</button>

      <div>
          <h3>Description:</h3>
          <p>{{product.description}}</p>
      </div>
    </div>
    <hr>
    <h3>Subtotal({{getCartLength}} items): ${{getCartTotalPrice}}</h3>
    <button>
      <nuxt-link to="/placeorder">Proceed to Checkout
    </nuxt-link></button>
    <nuxt-link to="/placeorder">
    </nuxt-link>
  </div>
</template>

<script>
import {mapGetters} from 'vuex';
export default {
  computed: {
    ...mapGetters(["getCart", "getCartTotalPrice", "getCartLength"])
  },
  methods: {
    onChangeQuantity(event, product){
      let qty = parseInt(event.target.value)
      this.$store.commit("changeQty", { product, qty });
    },

    checkQty(prodQty, qty){
      if(parseInt(prodQty) === parseInt(qty)){
        return true;
      } else {
        return false;
      }
    }
  },
}
</script>

<style scoped>
img{
  height: 300px;
  width: 250px;
}
</style>

<template>
<div class="order-page">
  <h2>Your Orders</h2>
  <div v-for="order in orders" :key="order._id">

    <h4>
      <NuxtLink :to="'/orderDetails/' + order._id">
      Order Id: {{order._id}}
      </NuxtLink>
      </h4>
    <div class="orders-products">
      <div class="product" v-for="product in order.products" :key="product._id">
        <h4>{{product.prodId.title}}</h4>
        <img :src="'http://localhost:5000/'+ product.prodId.photo" alt="">
        <!-- <p>Quantity:{{product.quantity}}</p>
        <p>Price: {{product.price}}</p> -->
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    try{
      let response = await $axios.$get('http://localhost:5000/order/allOrders');

      return {
        orders: response.products
      }
    }catch(err){
      console.log(err)
    }
  },
}
</script>

<style scoped>

a{
  text-decoration: none;
  color: rgb(87, 188, 231);
}
.order-page{
  margin: 20px;
}

.orders-products{
  border: 1px solid lightgray;
  padding: 20px;
}

</style>

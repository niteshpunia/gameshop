<template>
  <div>
    <div>
      <h3>OrderId:{{order._id}} </h3>
      <h3>Order Total: ${{orderTotal}}</h3>
      <div class="products">
        <div class="product" v-for="product in order.products" :key="product._id">
        <h4>{{product.prodId.title}}</h4>
        <img :src="'http://localhost:5000/'+ product.prodId.photo" alt="">
        <p>Quantity:{{product.quantity}}</p>
        <p>Price: {{product.price}}</p>
      </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params }){
    try{
      let response = await $axios.$get(`http://localhost:5000/order/orderDetails/${params.id}`)
      let orderTotal = 0;
      response.order.products.map((item) => {
        orderTotal = orderTotal + (item.quantity * item.price);
      })
      return{
        order: response.order,
        orderTotal: orderTotal
      }
  }catch(err){
      console.log(err)
    }
  }
}
</script>


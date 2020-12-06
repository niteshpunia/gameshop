<template>
  <div class="products">
     <div class="product" v-for="item in products" :key="item._id">
            <Product :product-id="item._id" :product-title="item.title"
            :product-price="item.price" :product-rating="item.rating"
            :product-photo="item.photo"
          />
        </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params}) {
    try{
      let response = await $axios.$get(`http://localhost:5000/product/getAllProducts/${params.id}`);
      return {
        products: response.products,
      }
    }catch(err){
      console.log(err);
    }
  }
}
</script>

<style scoped>
.products{
  display: flex;
  justify-content: space-around;
  padding: 20px;
  margin: 20px;
}
</style>

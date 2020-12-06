<template>
  <div>
    <h2>You Searched for..</h2>
    <div class="products">
      <div class="product" v-for="product in products" :key="product.objectID">
        <h3>{{product.title}}</h3>
        <NuxtLink :to="'/products/' + product.objectID">
            <img :src="'http://localhost:5000/'+ product.photo" alt="image">
        </NuxtLink>

        <h4>Price: ${{product.price}}</h4>
      </div>
    </div>
  </div>



</template>

<script>
export default {
  watchQuery: ["title"],

  async asyncData({ $axios, query }) {
    try{
      let products = await $axios.$post('http://localhost:5000/search/searchProduct',{ title: query.title})
      return {
        products
      }
     }catch(err){
       console.log(err);
    }
  },
}
</script>

<style scoped>
.product{
  border: 1px lightgray solid;
  margin: 10px;
  padding: 10px;
}
</style>

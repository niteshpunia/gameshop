<template>
<div>
  <h3>Product Details</h3>
  <div class="productDetails">
      <h3>{{product.title}}</h3>
      <h3>$ {{product.price}}</h3>
      <!-- <div>{{product.rating}}</div> -->
      <img class="prodImage" :src="'http://localhost:5000/'+ product.photo"/>
      <button @click="addProductToCart(product)">Add to Cart</button>
      <div class="productDesc">
          <h3>Description:</h3>
          <p>{{product.description}}</p>
      </div>
      </div>
      <div class="reviewSection">
        <ReviewSection :product="product" :reviews="reviews" />
      </div>


  </div>
</template>

<script>
 import ReviewSection from "~/components/ReviewSection";
 import { mapActions } from 'vuex';
export default {
 components: {
   ReviewSection
 },

  async asyncData({ $axios, params}) {
    try {
      let singleProduct = await $axios.$get(`http://localhost:5000/product/getProduct/${params.id}`);
      let reviews = await $axios.$get(`http://localhost:5000/review/allReviews/${params.id}`)

      return {
        product: singleProduct.product,
        reviews: reviews.reviews
      }
    }catch(err){
      console.log(err);
    }
  },

  methods: {
    ...mapActions(["addProductToCart"])
  },
}
</script>

<style>

.productDetails{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.prodImage{
  height: 400px;
  width: 300px;
}

.productDesc{
  margin: 20px;
}
.reviewSection{
  margin: 20px;
}
</style>

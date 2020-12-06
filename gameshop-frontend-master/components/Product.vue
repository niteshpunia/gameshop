 <template>
  <div>
       <NuxtLink :to="'/products/' + productId">
          <img :src="'http://localhost:5000/'+ productPhoto" alt="product-image"/>
        </NuxtLink>

      <h2>{{productTitle}}</h2>
      <!-- <div>{{productRating}}</div> -->
      <h3>${{productPrice}}</h3>
  </div>
</template>
<script>

export default {
    name: 'Product',
    props: ['productId','productPrice', 'productTitle', 'productRating', 'productPhoto']
}
</script>

<style scoped>
a, a:hover, a:focus, a:active{
  text-decoration: none;
  color: inherit;
}
img{
  height: 300px;
  width: 250px;
}
</style>

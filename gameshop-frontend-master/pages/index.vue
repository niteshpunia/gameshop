<template>
  <div class="home">
    <div class="search">
      <Search/>
    </div>
    <div class="categories">
      <Categories :categories="categories"/>
    </div>
    <div class="main">

        <img class="bannerImage" src="/banner.png"/>
    </div>

    <div>
        <h1 class="head">All the games u want to play are available here</h1>
        <div class="products">
          <div class="product" v-for="item in products.slice(0, 3)" :key="item._id">
            <Product :product-id="item._id" :product-title="item.title"
            :product-price="item.price" :product-rating="item.rating"
            :product-photo="item.photo"
          />
        </div>
    </div>

  </div>
  </div>
</template>

<script>
import Product from '../components/Product';
import Search from '../components/Search';
import Categories from '../components/Categories';
export default {
  name: 'Home',
  components: {
    Product,
    Search,
    Categories
  },

  async asyncData({$axios}){
    try{
      let response = await $axios.$get("http://localhost:5000/product/getAllProducts");
      let response2 = await $axios.$get("http://localhost:5000/category/getCategories");
      return {
        products: response.products,
        categories: response2.categories,
      }
    }catch(err){
      console.log(err);
    }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


.home{
  margin-bottom: 100px;
}

.search{
  display: flex;
  justify-content: center;
  margin: 10px;
}

.bannerImage{
  object-fit: contain;
  width: 100%;
}

.head {
  text-align: center;
  margin-top: 20px;
}

.products{
  display: flex;
  justify-content: space-around;
  margin: 30px;
}

.bottom-banner{
  display: flex;
  justify-content: space-around;
  margin-top: 80px;
}

.bottom-banner-child{
  display: flex;
  flex-direction: column;
  margin-bottom: 50px;
}

</style>

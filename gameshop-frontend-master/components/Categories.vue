<template>
    <div class="categorySection">
    <h5>Shop by Category</h5>
    <div class="categories">
    <div v-for="category in categories" :key="category._id">
      <NuxtLink :to="'/category/' + category._id">
      <h5>{{category.type}}</h5>
       </NuxtLink>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  props: ["categories"]

}
</script>

<style scoped>
h5{
  text-align: center;
}
.categorySection{
   background-color: rgb(55, 178, 206);
    padding: 10px;
}
.categories{
  display: flex;
  justify-content: space-around;

}
a{
  color: white;
  text-decoration: none;
}
</style>

<template>
  <div>
    <h1>Create Review</h1>
    <div>
      <h2>{{product.title}}</h2>
    </div>
    <!-- <div>
      <h2>Overall Rating</h2>
      <no-ssr placeholder="loading...">
      <StarRating v-model="rating"></StarRating>
      </no-ssr>
    </div> -->
    <form>
  <div class="form-group">
    <label for="headline">Add a Headline</label>
    <input type="text" v-model="headline" class="form-control" id="headline" >
  </div>

  <div class="form-group">
    <label for="body">Write your Review</label>
    <input type="text" v-model="body" class="form-control" id="body">
  </div>

    <div class="form-group">
    <label for="name">Your Name</label>
    <input type="text" :value="$auth.$state.user.name" class="form-control" id="name">
  </div>

  <button type="submit" class="btn btn-primary" @click="onAddReview">Submit</button>
</form>
  </div>
</template>

<script>
// import StarRating from "vue-star-rating";
export default {
  components: {
    // StarRating
  },
  async asyncData({ $axios, params }) {
    try{
      let response = await $axios.$get(`http://localhost:5000/product/getProduct/${params.id}`);
      return {
        product: response.product
      }

    }catch(err){
      console.log(err)
    }
  },
  data(){
    return {
      rating: 0,
      body: "",
      headline: "",
    }
  },

  methods: {
    async onAddReview(e){
      e.preventDefault();
      try{
        let data = {
          headline: this.headline,
          body: this.body
        }

        let response = await this.$axios.$post(
          `http://localhost:5000/review/addReview/${this.$route.params.id}`,
          data
        );

        if(response.success){
          this.$router.push(`/products/${this.$route.params.id}`);
        }

      }catch(err){
        console.log(err);
      }
    }
  }

}
</script>

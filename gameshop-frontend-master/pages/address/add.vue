<template>
  <div>
     <form class="address">
     <h3>Enter your Address</h3>
    <div class="form-group">
    <label for="fullName">Fullname</label>
    <input type="text" v-model="fullName" class="form-control" id="fullName">
    </div>

  <div class="form-group">
    <label for="country">Country</label>
    <input type="text" v-model="country" class="form-control" id="country" >
  </div>

    <div class="form-group">
    <label for="streetAddress">Street Address</label>
    <input type="text" v-model="streetAddress" class="form-control" id="streetAddress" >
  </div>

      <div class="form-group">
    <label for="city">City</label>
    <input type="text" v-model="city" class="form-control" id="city" >
  </div>

    <div class="form-group">
    <label for="state">State</label>
    <input type="text" v-model="state" class="form-control" id="state" >
  </div>

      <div class="form-group">
    <label for="zipCode">Zip Code</label>
    <input type="text" v-model="zipCode" class="form-control" id="zipCode" >
  </div>

    <div class="form-group">
    <label for="phoneNumber">Phone Number</label>
    <input type="text" v-model="phoneNumber" class="form-control" id="phoneNumber" >
  </div>

      <div class="form-group">
    <label for="deliverInstructions">Delivery Instructions</label>
    <input type="text" v-model="deliverInstructions" class="form-control" id="deliverInstructions" >
  </div>


    <div class="form-group">
    <label for="securityCode">Security Code</label>
    <input type="text" v-model="securityCode" class="form-control" id="securityCode" >
  </div>


  <button type="submit" class="btn btn-primary" @click="onAddAddress">Submit</button>
  </form>
  </div>
</template>

<script>
export default {

  data(){
    return {
        fullName: "",
        country: "",
        streetAddress: "",
        city: "",
        state: "",
        zipCode: "",
        phoneNumber: "",
        deliverInstructions: "",
        securityCode: ""
    };
  },

  methods: {
    async onAddAddress(e) {
      e.preventDefault();
      try{
        let data = {
        fullName: this.fullName,
        country: this.country,
        streetAddress: this.streetAddress,
        city: this.city,
        state: this.state,
        zipCode: this.zipCode,
        phoneNumber: this.phoneNumber,
        deliverInstructions: this.deliverInstructions,
        securityCode: this.securityCode
      }
      let response = await this.$axios.$post('http://localhost:5000/address/addAddress', data);

      if(response.success){
        this.$router.push('/');
      }

      }catch(err){
        console.log(err);
      }

    }
  }
}
</script>

<style scoped>
.address{
  margin: 20px;
  padding: 20px;
  border: 1px solid lightgray;
  margin-left: auto;
  margin-right: auto;
  width: 800px;
}
</style>

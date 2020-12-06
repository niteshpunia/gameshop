<template>
  <div>
    <div class="userDetails">
      <h4>User Details</h4>
      <p>Name: {{$auth.$state.user.name}}</p>
      <p>Email: {{$auth.$state.user.email}}</p>
    </div>
    <div class="userAddress">
      <h4>User Address</h4>
      <template v-if="addresses.length < 1">
        <p>Please enter the address, by pressing the button below.</p>
      <button>
        <nuxt-link to="/address/add">
          Add Address
        </nuxt-link>
        </button>
      </template>
      <template v-else>
      <p>Full Name:{{addresses[0].fullName}}</p>
      <p>Country: {{addresses[0].country}}</p>
      <p>Street Address: {{addresses[0].streetAddress}}</p>
      <p>City: {{addresses[0].city}}</p>
      <p>State: {{addresses[0].state}}</p>
      <p>ZipCode: {{addresses[0].zipCode}}</p>
      <p>Phone Number: {{addresses[0].phoneNumber}}</p>
      <p>Delivery Instructions: {{addresses[0].deliverInstructions}}</p>
      <p>Security Code: {{addresses[0].securityCode}}</p>
      <span>
        <nuxt-link to="">Edit</nuxt-link>
        <nuxt-link to="">Delete</nuxt-link>
      </span>
      </template>

    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params}){
    try{
      let response = await $axios.$get('http://localhost:5000/address/getAddresses');

      return {
        addresses: response.addresses
      }
    }catch(err){
      console.log(err);
    }
  }
}
</script>

<style scoped>
.userDetails{
  margin: 30px;
}
.userAddress{
  margin: 30px;
  border: 1px solid lightgray;
  padding: 10px;
}
</style>

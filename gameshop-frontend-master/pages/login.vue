<template>
<div>
    <form class="login">

  <div class="form-group">
    <label for="email">Email address</label>
    <input type="email" v-model="email" class="form-control" id="email" >
  </div>

  <div class="form-group">
    <label for="password">Password</label>
    <input type="password" v-model="password" class="form-control" id="password">
  </div>

  <button type="submit" class="btn btn-primary" @click="onLogin">Login</button>
  <p>Don't have an Account? </p>
<nuxt-link to="/signup">Register Here</nuxt-link>
</form>

</div>

</template>

<script>
 export default {
   middleware: "auth",
   auth: "guest",
  //  above two line are added to redirect the user back to homepage if he tries to visit the login page again after once logged in.
    name: 'Signup',
    data(){
      return {
        name: "",
        email: "",
        password: "",
      };
    },
    methods: {
      async onLogin(e){
        e.preventDefault();
        try{
            this.$auth.loginWith("local", {
              data: {
                email: this.email,
                password: this.password
              }
            });

            this.$router.push("/");


        }catch(err){
          console.log(err);
        }
      }
    }
    }
</script>

<style scoped>
.login{
  border: 1px solid lightgray;
  border-radius: 10px;
  padding: 50px;
  margin: 20px;
  display: flex;
  flex-direction: column;
  width: 400px;
  justify-content: center;
  margin-left: auto;
  margin-right: auto;
}
</style>

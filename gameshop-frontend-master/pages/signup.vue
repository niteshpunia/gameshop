<template>
<div>
    <form class="register">
    <div class="form-group">
    <label for="name">Name</label>
    <input type="text" v-model="name" class="form-control" id="name">
    </div>

  <div class="form-group">
    <label for="email">Email address</label>
    <input type="email" v-model="email" class="form-control" id="email" >
  </div>

  <div class="form-group">
    <label for="password">Password</label>
    <input type="password" v-model="password" class="form-control" id="password">
  </div>

  <div class="form-group">
    <label for="confirmPassword">Confirm-Password</label>
    <input type="password" class="form-control" id="confirmPassword">
  </div>

  <button type="submit" class="btn btn-primary" @click="onSignup">Submit</button>

    <p>Already have an Account? </p>
<nuxt-link to="/login">Login into your account</nuxt-link>
</form>
</div>
</template>

<script>
 export default {
    name: 'Signup',
   middleware: "auth",
   auth: "guest",

    data(){
      return {
        name: "",
        email: "",
        password: "",
      };
    },
    methods: {
      async onSignup(e){
        e.preventDefault();
        try{
          let data = {
            name: this.name,
            email: this.email,
            password: this.password,
          }

          let response = await this.$axios.$post('http://localhost:5000/user/auth/signup', data);
          console.log(response);

          if(response.success){
            this.$auth.loginWith("local", {
              data: {
                email: this.email,
                password: this.password
              }
            });

            this.$router.push("/");
          }

        }catch(err){
          console.log(err);
        }
      }
    }
    }
</script>

<style scoped>
.register{
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

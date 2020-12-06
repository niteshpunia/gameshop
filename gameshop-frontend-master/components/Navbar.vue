<template>
    <div>
  <b-navbar toggleable="lg" type="dark" variant="info">
    <b-navbar-brand>

          <NuxtLink to="/">
        Brutal-X
          </NuxtLink></b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
              <b-navbar-nav>
              <template v-if="$auth.$state.loggedIn">
               <b-nav-item> Hello, {{$auth.$state.user.name}} </b-nav-item>



            <b-nav-item>
               <nuxt-link to="/profile">
               Profile
            </nuxt-link>
              </b-nav-item>
              <b-nav-item>
                 <a to="/" @click="onLogout">
              Logout
            </a>
            </b-nav-item>
              </template>
              <template v-else>
                 <b-nav-item>
              <nuxt-link to="/login">
              Login
            </nuxt-link>
            </b-nav-item>
              </template>

            <b-nav-item>
          <nuxt-link to="/cart">
           Cart ({{getCartLength}})
            </nuxt-link>
            </b-nav-item>

                     <b-nav-item>
          <nuxt-link to="/orders">
           My Orders
            </nuxt-link>
            </b-nav-item>


      </b-navbar-nav>

      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
  <!-- <Search/> -->
</div>
</template>

<script>
import { mapGetters } from "vuex";
import Search from './Search';
export default {
  name: 'Navbar',
  components: {
    Search,
  },

  computed: {
    ...mapGetters(["getCartLength"])
  },

  methods:{
      async onLogout(){
    await this.$auth.logout();
  }
  }

}
</script>

<style scoped>
a, a:hover, a:focus, a:active{
  text-decoration: none;
  color: inherit;
}

</style>

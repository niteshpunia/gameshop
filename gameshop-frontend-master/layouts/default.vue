<template>
  <div class="main">
    <Navbar/>
    <Nuxt />
    <!-- <Footer/> -->
  </div>
</template>

<script>
import Navbar from "~/components/Navbar";
import Footer from "~/components/Footer";
export default {
    components: {
      Navbar,
      Footer
    },
}
</script>

<style>
html, body {
  height: 100%;
}
#main{
    display: flex;
  flex-direction: column;
  height: 100%;

}
</style>


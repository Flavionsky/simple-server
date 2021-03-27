<template>
  <div id="app">
  <Navbar></Navbar>
  <Home msg="Benvenuto nella pagina di scelta dei server"/>
  <Custom></Custom>
  </div>
</template>

<style lang="scss">
#app {
  font-family: "Orbitron", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

</style>

<script>
import Navbar from '@/components/Navbar.vue'
import Home from '@/components/Home.vue'
import Custom from '@/components/Custom.vue'
export default {
  components: {
    Home,
    Navbar,
    Custom
  }
}
</script>
<template>
  <div id="app">
    <Navbar></Navbar>
    <Home msg="Benvenuto nella pagina di scelta dei server" />
    <Custom></Custom>
    <footer>
      <b-container>
        <b-row align-h="around">
          <b-col class="d-flex justify-content-center align-items-center" lg="3" md="6" sm="12">
            <p class="m-0">&copy; Flavio Muscente</p>
          </b-col>
        </b-row>
      </b-container>
  </footer>
  </div>
</template>

<style lang="scss">
#app {
  font-family: "Orbitron", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  footer{
      display: flex;
      align-items: center;
      justify-content: flex-start;
      background-color: #17A2B8;
      color: white;
      font-size: 22px;
      height: 10vh;
  }
}
</style>

<script>
import Navbar from "@/components/Navbar.vue";
import Home from "@/components/Home.vue";
import Custom from "@/components/Custom.vue";
export default {
  components: {
    Home,
    Navbar,
    Custom,
  },
  methods: {
    goto(refName) {
      var element = this.$refs[refName];
      var top = element.offsetTop;
      window.scrollTo(0, top);
    },
  },
};
</script>
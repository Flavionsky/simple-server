<template>
    <b-navbar class="nav-bar" toggleable="lg" type="light" variant="info">
      <b-navbar-brand href="#">
        <div class="left-logo">
          <img src="img/logo.png" alt="Logo" />
          <span>YourVPS</span>
        </div>
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse">
        <!-- Collapse button -->
        <button id="nav-btn" @click="clicked = !clicked">
          <div class="animated-icon1" :class="[clicked ? 'open' : '']">
            <span></span><span></span><span></span>
          </div>
        </button>
      </b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item right>
           <button id="goToCustom" v-if="windowWidth < 991" @click="clicked = !clicked" v-scroll-to="'#custom'">Server Custom</button>
           <button id="goToCustom" v-else v-scroll-to="'#custom'"><span>{{clicked = false}}</span>Server Custom</button>  
          </b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
</template>

<script>
export default {
  name: "Navbar",
  data: function () {
    return {
      clicked: false,
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.nav-bar {
  position: fixed;
  z-index: 100;
  width: 100%;
  top: 0;
  .left-logo {
    display: flex;
    align-items: center;
    justify-content: center;
    img {
      width: 60px;
    }
    span {
      color: white;
    }
  }
  button{
    font-size: 20px;
  }
  #goToCustom{
    border: 1px solid black;
    background: white;
    border-radius: 10px;
    box-shadow: 0 0 10px black;
    span{
      display: none;
    }
  }
}
#nav-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: none !important;
  height: 38px;
  border: none;
  background: none;
}
.animated-icon1 {
  width: 30px;
  height: 20px;
  position: relative;
  margin: 0px;
  -webkit-transform: rotate(0deg);
  -moz-transform: rotate(0deg);
  -o-transform: rotate(0deg);
  transform: rotate(0deg);
  -webkit-transition: 0.5s ease-in-out;
  -moz-transition: 0.5s ease-in-out;
  -o-transition: 0.5s ease-in-out;
  transition: 0.5s ease-in-out;
  cursor: pointer;
  span {
    display: block;
    position: absolute;
    height: 3px;
    width: 100%;
    border-radius: 10px;
    opacity: 1;
    left: 0;
    -webkit-transform: rotate(0deg);
    -moz-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
    -webkit-transition: 0.25s ease-in-out;
    -moz-transition: 0.25s ease-in-out;
    -o-transition: 0.25s ease-in-out;
    transition: 0.25s ease-in-out;
    background: white;
    &:nth-child(1) {
      top: 0px;
    }
    &:nth-child(2) {
      top: 10px;
    }
    &:nth-child(3) {
      top: 20px;
    }
  }
}
.animated-icon1.open {
  span {
    &:nth-child(1) {
      top: 11px;
      -webkit-transform: rotate(135deg);
      -moz-transform: rotate(135deg);
      -o-transform: rotate(135deg);
      transform: rotate(135deg);
    }
    &:nth-child(2) {
      opacity: 0;
      left: -60px;
    }
    &:nth-child(3) {
      top: 11px;
      -webkit-transform: rotate(-135deg);
      -moz-transform: rotate(-135deg);
      -o-transform: rotate(-135deg);
      transform: rotate(-135deg);
    }
  }
}
button.navbar-toggler.collapsed,
button.navbar-toggler.not-collapsed {
  padding: 2px;
  border: none;
}
@media screen and (max-width: 350px) {
  .nav-bar {
    .left-logo {
      img {
        width: 38px;
      }
      span {
        font-size: 15px;
      }
    }
  }
}
@media screen and (max-width: 350px) {
  .nav-bar {
    .left-logo {
      img {
        width: 38px;
      }
      span {
        font-size: 15px;
      }
    }
  }
}
</style>

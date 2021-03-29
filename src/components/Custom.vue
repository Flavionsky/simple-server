<template>
  <div>
    <b-container class="offers">
      <b-row align-h="around">
        <b-col lg="6" md="6" sm="12" class="server-card">
          <h2>CUSTOM</h2>
          <div class="property">
            <span class="element" v-for="(element, index) in elements" :key="index">
              <img :src="element.img_url" alt="element" />
              <br>
              <span>{{ element.qty + element.min }}</span>
              <span v-if="element.name == 'cpu'"> Core</span>
              <span v-if="element.name == 'hd' || element.name == 'ram'"> GB</span>
              <span>
                <br>
                <button @click="addItem(element)" @mousedown="delayUp(element)" @mouseup="stop()" @mouseleave="stop()"><i class="fas fa-plus"></i></button>
                <button @click="minusQty(element)" @mousedown="delayDown(element)" @mouseup="stop()" @mouseleave="stop()"><i class="fas fa-minus"></i></button>
              </span>
            </span>
          </div>
          <div class="nas">
            <img src="img/nas.webp" alt="nas" />
            <label>
              <span :class="{visible:(nas==27)}">Si<input type="radio" name="nas" v-model="nas" :value="27" /></span>
              <span :class="{visible:(nas==0)}">No<input type="radio" name="nas" v-model="nas" :value="0" /></span>
            </label>
          </div>
          <ul class="os">
            <li :class="{visible:(windows==10)}">
              <label>
                <img class="windows-img" src="img/windows-small.svg" alt="windows" />
                <h5>Windows</h5>
                <input type="radio" name="windows" v-model="windows" :value="10" />
              </label>
            </li>
            <li :class="{visible:(windows==0)}">
            <label>
              <img class="centos-img" src="img/centos-small.png" alt="centos" />
              <h5>CentOS</h5>
              <input type="radio" name="windows" v-model="windows" :value="0" />  
            </label>
            </li>
          </ul>
          <div class="price">
            <p>totale: {{ total() }} &#8364;</p>
            <p>+ IVA/mese</p>
            <button>Ordina adesso</button>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "Custom",
  data: function () {
    return {
      elements: [
        {
          id: 1,
          name: "cpu",
          img_url: "img/cpu.png",
          qty: 0,
          eachqty: 1,
          price: 20,
          min: 1,
          max: 7,
          total: 0,
        },
        {
          id: 2,
          name: "ram",
          img_url: "img/ram.webp",
          qty: 0,
          eachqty: 1,
          price: 3,
          min: 1,
          max: 15,
          total: 0,
        },
        {
          id: 3,
          name: "hd",
          img_url: "img/hdd.png",
          qty: 0,
          eachqty: 10,
          price: 0.35,
          min: 50,
          max: 450,
          total: 0,
        },
        {
          id: 4,
          name: "ip",
          img_url: "img/ip.png",
          qty: 0,
          eachqty: 1,
          price: 5,
          min: 1,
          max: 4,
          total: 0,
        },
      ],
      timeout: null,
      nas: 0,
      windows: 0,
    };
  },
  methods: {
    addItem: function (element) {
      var isInArray = this.elements.find((e) => e.id === element.id);
      if (isInArray) {
        this.elements.forEach(function (e) {
          if (e.id === element.id) {
            if (e.qty < e.max) {
              e.qty += e.eachqty;
              e.total = (e.qty * e.price).toFixed(2);
            }
          }
        });
      }
    },
    delayUp(element) {
      this.timeout = setInterval(() => {
        this.addItem(element);
      }, 150);
    },
    delayDown(element) {
      this.timeout = setInterval(() => {
        this.minusQty(element);
      }, 150);
    },
    minusQty: function (element) {
      this.elements.forEach(function (e) {
        if (e.id === element.id && e.id != 3) {
          if (e.qty >= e.min) {
            e.qty -= e.eachqty;
            e.total = (e.qty * e.price).toFixed(2);
          }
        }
        if (e.id === 3 && e.qty > 0) {
              e.qty -= 10;
              e.total = (e.qty * e.price).toFixed(2);
        }
      });
    },
    // returns the updated total after each addition or subtraction performed on element
    total: function () {
      var sum = 80 + this.nas + this.windows;
      this.elements.forEach(function (element) {
        sum += parseFloat(element.total);
      });
      return sum.toFixed(2);
    },
    stop() {
      // clear the interval when mouse leave or mouse up
      clearInterval(this.timeout);
      this.timeout = null;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit SCSS to this component only -->
<style scoped lang="scss">
ul {
  list-style: none;
}
.visible{
  opacity: 1 !important;
  box-shadow: 0 0 20px black;
}
.offers {
  .server-card {
    margin-top: 80px;
    padding-top: 10px;
    color: whitesmoke;
    background-image: url("/img/property.jpg");
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
    border-radius: 15px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    h2{
      padding-bottom: 30px;
    }
    .property {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      align-items: center;
      .element {
        padding-right: 20px;
        img {
          width: 94px;
          padding-right: 10px;
          padding-bottom: 20px;
        }
        span{
          button{
            margin-top: 20px;
            margin-right:16px;
          }
        }
      }
    }
    .price {
      p:first-child {
        font-size: 40px;
        text-shadow: 0 0 20px black;
      }
      p:last-child {
        font-size: 14px;
        margin-top: -16px;
        text-shadow: 0 0 20px black;
      }
    }
    button {
      background-color: #072549;
      padding: 5px;
      margin-bottom: 10px;
      color: whitesmoke;
      border: 1px solid white;
      border-radius: 10px;
    }
    .extreme-btn {
      margin-top: -5px;
    }
    .nas{
      margin-top: 30px;
      margin-bottom: 10px;
      width: 140px;
      display: flex;
      flex-direction: column;
      align-items: center;
      img{
        width: 120px;
      }
      span{
        position: relative;
        font-size: 22px;
        padding: 5px;
        margin: 5px;
        opacity: 0.5;
        border-radius: 10px;
        input{
          position: absolute;
          left: 0;
          top: 0;
          opacity: 0;
          cursor: pointer;
          width: 90%;
          height: 80%;
          display: inline-block;
        }
      }
    }
    .os{
      display: flex;
      li{
        position: relative;
        width: 120px;
        height: 150px;
        border-radius: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        opacity: 0.5;
        .windows-img{
          width: 90px;
        }
        .centos-img{
          width: 110px;
        }
        input{
          position: absolute;
          left: 0;
          top: 0;
          opacity: 0;
          cursor: pointer;
          width: 100%;
          height: 100%;
          display: inline-block;
        }
      }
      li:first-child{
        h5{
          padding-top: 10px;
          margin-bottom: 0px;
        }
      }
    }
  }
}
</style>

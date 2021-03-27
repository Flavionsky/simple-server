<template>
  <div class="home">
    <header>
      <h1>Ordina adesso a partire da 80&#8364;/mese!</h1>
    </header>
    <main>
      <b-container class="offers">
        <b-row align-h="around">
          <b-col lg="3" md="4" sm="12" class="server-card">
            <h3>STANDARD</h3>
            <div class="property">
              <span><img src="img/cpu.png" alt="cpu" /> 1 Core</span>
              <span><img src="img/ram.webp" alt="ram" />1 GB</span>
              <span><img src="img/hdd.png" alt="rhdd" />50 GB</span>
              <span><img src="img/ip.png" alt="ip" />1</span>
              <span><img src="img/centos.png" alt="os" /></span>
            </div>
            <div class="price">
              <p>80 &#8364;</p>
              <p>+ IVA/mese</p>
            </div>
            <button>Ordina adesso</button>
          </b-col>
          <b-col lg="3" md="4" sm="12" class="server-card">
            <h3>MEDIUM</h3>
            <div class="property">
              <span><img src="img/cpu.png" alt="cpu" /> 4 Core</span>
              <span><img src="img/ram.webp" alt="ram" />8 GB</span>
              <span><img src="img/hdd.png" alt="rhdd" />250 GB</span>
              <span><img src="img/ip.png" alt="ip" />3</span>
              <span><img src="img/windows2016.png" alt="os" /></span>
            </div>
            <div class="price">
              <p>188 &#8364;</p>
              <p>+ IVA/mese</p>
            </div>
            <button>Ordina adesso</button>
          </b-col>
          <b-col lg="3" md="4" sm="12" class="server-card">
            <h3>EXTREME</h3>
            <div class="property">
              <span><img src="img/cpu.png" alt="cpu" />8 Core</span>
              <span><img src="img/ram.webp" alt="ram" />16 GB</span>
              <span><img src="img/hdd.png" alt="rhdd" />500 GB</span>
              <span><img src="img/ip.png" alt="ip" />5</span>
              <span><img src="img/windows2016.png" alt="os" /></span>
              <span><img src="img/nas.webp" alt="nas" /></span>
            </div>
            <div class="price">
              <p>337,75 &#8364;</p>
              <p>+ IVA/mese</p>
            </div>
            <button class="extreme-btn">Ordina adesso</button>
          </b-col>
        </b-row>
      </b-container>
    </main>
  </div>
</template>

<script>
export default {
  name: "Home",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.home {
  padding-top: 86px;
  header {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100vw;
    height: 40vh;
    background-image: url("/img/header.jpg");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    h1 {
      color: white;
    }
  }
  main {
    .offers {
      .server-card {
        margin-top: 80px;
        padding-top: 10px;
        color: whitesmoke;
        background-image: url("/img/property.jpg");
        background-position: center;
        border-radius: 15px;
        .property {
          display: flex;
          flex-wrap: wrap;
          justify-content: flex-start;
          span {
            &:nth-child(1) {
              margin-left: -6px;
              padding-bottom: 10px;
            }
            &:nth-child(2) {
              padding-left: 20px;
            }
            &:nth-child(4) {
              padding-left: 26px;
            }
            &:nth-child(5) {
              img {
                height: 70px;
                width: 140px;
              }
            }
            &:nth-child(6) {
              img {
                width: 80px;
              }
            }
            padding-left: 5px;
            padding-top: 20px;
            img {
              width: 60px;
              padding-right: 5px;
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
        button{
          background-color: #072549;
          padding: 5px;
          margin-bottom: 10px;
          color: whitesmoke;
          border: 1px solid white;
          border-radius: 10px;
        }
        .extreme-btn{
          margin-top: -5px;
        }
      }
    }
  }
}
@media screen and (max-width: 770px) {
  header {
    h1 {
      font-size: 32px;
    }
  }
}
@media screen and (max-width: 380px) {
  .home {
    padding-top: 64px;
  }
  header {
    h1 {
      font-size: 20px;
    }
  }
}
</style>

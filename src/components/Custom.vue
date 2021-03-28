<template>
  <div>
    <ul>
      <li v-for="(element, index) in elements" :key="index">
        <h3>{{ element.name }}</h3>
        <p>
          quantit&#224;: {{ element.qty + element.min }}
          <span v-if="element.name == 'hd'"
            >GB <button @click="addItem(element)" @mousedown="delayUp(element)" @mouseup="stop()" @mouseleave="stop()">+10 GB</button>
            <button @click="minusQty(element)" @mousedown="delayDown(element)" @mouseup="stop()" @mouseleave="stop()">-10 GB</button></span
          >
          <span v-else
            ><button @click="addItem(element)" @mousedown="delayUp(element)" @mouseup="stop()" @mouseleave="stop()">+1</button>
            <button @click="minusQty(element)" @mousedown="delayDown(element)" @mouseup="stop()" @mouseleave="stop()">-1</button></span
          >
        </p>
        <p>prezzo: {{ element.price }} &#8364;</p>
      </li>
    </ul>
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
          qty: 0,
          eachqty: 1,
          price: 20,
          min: 1,
          max: 7,
          total: 0
        },
        {
          id: 2,
          name: "ram",
          qty: 0,
          eachqty: 1,
          price: 3,
          min: 1,
          max: 15,
          total: 0
        },
        {
          id: 3,
          name: "hd",
          qty: 0,
          eachqty: 10,
          price: 0.35,
          min: 50,
          max: 450,
          total: 0
        },
        {
          id: 4,
          name: "ip",
          qty: 0,
          eachqty: 1,
          price: 5,
          min: 1,
          max: 4,
          total: 0
        },
      ],
      timeout: null
    };
  },
  methods: {
    addItem: function (element) {
        var isInArray = this.elements.find((e) => e.id === element.id);
        if (isInArray) {
          this.elements.forEach(function (e) {
            if (e.id === element.id && e.id != 3) {
              if (e.qty < e.max) {
                e.qty += e.eachqty;
                e.total = (e.qty * e.price).toFixed(2);
              }
            }
            if (e.id === element.id && e.id === 3) {
              if (e.qty < e.max) {
                e.qty += e.eachqty;
                e.total = ((e.qty * e.price) / 10).toFixed(2);
              }
            }
          });
        }
      
    },
    delayUp (element) {
        // Re-enable after 5 seconds
        this.timeout = setInterval(() => {
        this.addItem(element);
        }, 150)

      },
      delayDown (element) {
        // Re-enable after 5 seconds
        this.timeout = setInterval(() => {
        this.minusQty(element);
        }, 150)

      },
    removeItem: function (element) {
      var index = this.elements.indexOf(element);
      this.elements.splice(index, 1);
    },
    minusQty: function (element) {
      this.elements.forEach(function (e) {
        if (e.id === element.id && e.id != 3) {
          if (e.qty >= e.min) {
            e.qty -= e.eachqty;
            e.total = (e.qty * e.price).toFixed(2);
          }
        }
        if (e.id === element.id && e.id === 3) {
          if (e.qty >= e.min) {
            e.qty -= e.eachqty;
            e.total = ((e.qty * e.price) / 10).toFixed(2);
          }else{
              if(e.qty > 0){
                  e.qty -= 10;
              }
          }
        }
      });
    },
    total: function () {
      var sum = 80;
      this.elements.forEach(function (element) {
        sum += parseFloat(element.total);
      });
      return sum.toFixed(2);
    },
   stop() {
     // clear the timeout before the component is destroyed
     clearInterval(this.timeout)
     this.timeout = null;
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
ul {
  list-style: none;
}
i {
  border: 1px solid black;
  padding: 10px;
  cursor: pointer;
}
</style>

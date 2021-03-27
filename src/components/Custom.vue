<template>
  <div>
    <ul>
      <li v-for="(element, index) in elements" :key="index">
        <h3>{{ element.name }}</h3>
        <p>
          quantit&#224;: {{ element.eachqty }}
          <span v-if="element.name == 'hd'"
            >GB <i @click="addItem(element)">+10 GB</i
            ><i @click="minusQty(element)">-10 GB</i></span
          >
          <span v-else
            ><i @click="addItem(element)">+ 1</i
            ><i @click="minusQty(element)">-1</i></span
          >
        </p>
        <p>prezzo: {{ element.price }} &#8364;</p>
      </li>
    </ul>
    <div v-if="selectedElements.length">
      <div v-for="(selectedEl, index) in selectedElements" :key="index">
        <h3>{{ selectedEl.name }}</h3>
        <p>
          {{ selectedEl.qty + selectedEl.min }}
        </p>
      </div>
      <p>totale: {{ total() }} &#8364;</p>
    </div>
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
          qty: 1,
          eachqty: 1,
          price: 20,
          min: 1,
          max: 7,
        },
        {
          id: 2,
          name: "ram",
          qty: 1,
          eachqty: 1,
          price: 3,
          min: 1,
          max: 15,
        },
        {
          id: 3,
          name: "hd",
          qty: 10,
          eachqty: 10,
          price: 0.35,
          min: 50,
          max: 450,
        },
        {
          id: 4,
          name: "ip",
          qty: 1,
          eachqty: 1,
          price: 5,
          min: 1,
          max: 4,
        },
      ],
      selectedElements: [],
    };
  },
  methods: {
    addItem: function (element) {
      if (this.selectedElements.length < 1) {
        this.pushData(element);
      } else {
        var isInArray = this.selectedElements.find((e) => e.id === element.id);
        if (isInArray) {
          this.selectedElements.forEach(function (e) {
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
        } else {
          this.pushData(element);
        }
      }
    },
    pushData: function (element) {
      this.selectedElements.push({
        id: element.id,
        name: element.name,
        qty: element.qty,
        price: element.price,
        eachqty: element.eachqty,
        max: element.max,
        min: element.min,
        total: element.price,
      });
    },
    removeItem: function (element) {
      var index = this.selectedElements.indexOf(element);
      this.selectedElements.splice(index, 1);
    },
    minusQty: function (element) {
      this.selectedElements.forEach(function (e) {
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
      this.selectedElements.forEach(function (element) {
        sum += parseFloat(element.total);
      });
      return sum.toFixed(2);
    },
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

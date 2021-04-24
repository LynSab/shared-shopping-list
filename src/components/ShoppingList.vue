<template>
  <div>
    <h1>Our List</h1>
    <div v-for="item in shoppingList" :key="item.name">
      <input type="checkbox" checked="false" />
      {{ item.name }} £{{ formatPrice(item.price) }}
    </div>
    <div>
      <input type="text" v-model="newItemName" v-on:keyup.enter="createItem" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'ShoppingList',
  props: {
    msg: String
  },
  data: function () {
    return {
      shoppingList: [ 
        {
          name: 'milk',
          price: 0.87,
          complete: false
        },
        {
          name: 'bread',
          price: 1.00,
          complete: false
        },
        {
          name: 'coffee',
          price: 1.75,
          complete: false
        },
        {
          name: 'vodka',
          price: 18.00,
          complete: false
        },
      ],
      newItemName: ""
    }
  },
  methods: {
    formatPrice: function(price) {
      return price.toFixed(2);
    },
    createItem: function() {
      const newItem = {
        name: this.newItemName,
        price: 0.00,
        complete: false
      };
      this.shoppingList.push(newItem)
      console.log(newItem)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
padding: 5px;
}
</style>

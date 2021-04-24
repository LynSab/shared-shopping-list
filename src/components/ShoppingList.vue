<template>
  <v-container>
    <v-row>
      <v-col sm="12" xs="12" md="12" lg="4" xl="4">
        <v-card
          class="mx-auto"
          tile
        >
          <v-list dense>
            <v-subheader>Our list</v-subheader>
            <v-list-item
              v-for="(item, index) in shoppingList" :key="index"
            >
              <v-badge
                dot
                inline
                left
                :color="priorityColour(item.priority)"
              ></v-badge>

              <input type="checkbox" checked="false" />

              <v-list-item-content>
                <v-list-item-title> {{ item.name }} </v-list-item-title>
              </v-list-item-content>

              <v-list-item-content>
                <v-list-item-title>£{{ formatPrice(item.price) }}</v-list-item-title> 
              </v-list-item-content>

              <v-list-item-icon>
                <v-icon dense @click="editItem(index)"> mdi-pencil </v-icon>
              </v-list-item-icon>

              <v-list-item-icon class="ml-1">
                <v-icon dense @click="removeItem(index)"> mdi-close </v-icon>
              </v-list-item-icon>

            </v-list-item>
          </v-list>
          <v-text-field
            v-model="newItemName"
            label="Outlined"
            outlined
            clearable
            v-on:keyup.enter="createItem"
          ></v-text-field>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
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
          owner: ["Steven", "Lyn"],
          priority: "high",
          complete: false
        },
        {
          name: 'bread',
          price: 1.00,
          owner: ["Steven"],
          priority: "medium",
          complete: false
        },
        {
          name: 'coffee',
          price: 1.75,
          owner: ["Lyn"],
          priority: "high",
          complete: false
        },
        {
          name: 'vodka',
          price: 18.00,
          owner: ["Steven", "Lyn"],
          priority: "low",
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
        owner: [],
        priority: "medium",
        complete: false
      };
      this.shoppingList.push(newItem)
      console.log(newItem)
    },
    removeItem: function(index) {
      this.shoppingList.splice(index,1)
    },
    editItem: function() {

    },
    priorityColour: function(priority) {
      if(priority=="high"){
        return "red"
      }
      if(priority=="medium"){
        return "orange"
      }
      if(priority=="low"){
        return "green"
      }
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

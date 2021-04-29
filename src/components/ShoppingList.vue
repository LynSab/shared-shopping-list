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
            <v-container v-for="(item, index) in shoppingList" :key="index">
              <v-row>
                <v-col>
                  <v-list-item                  >
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

                    <v-list-item-icon class="ml-1">
                      <v-icon dense @click="removeItem(index)"> mdi-close </v-icon>
                    </v-list-item-icon>

                    <v-list-item-icon class="ml-1">
                      <v-icon dense @click="item.showPanel = !item.showPanel"> {{ item.showPanel ? 'mdi-chevron-up' : 'mdi-chevron-down' }} </v-icon>
                    </v-list-item-icon>
                  </v-list-item>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <v-expand-transition>
                    <div v-show="item.showPanel">
                      <v-divider></v-divider>

                      <v-card-text>
                        <v-list-item>
                          <v-list-item-content>
                            Price: £{{ formatPrice(item.price) }}
                          </v-list-item-content>
                          <div class="text-center">
                            <v-dialog
                              v-model="item.showEdit"
                              width="500"
                            >
                              <template v-slot:activator="{ on, attrs }">
                                <v-btn
                                  v-bind="attrs"
                                  v-on="on"
                                  icon
                                  x-small
                                >
                                  <v-icon dense> mdi-pencil </v-icon>
                                </v-btn>
                              </template>

                              <v-card>
                                <v-card-title class="headline grey lighten-2">
                                  Edit
                                </v-card-title>

                                <v-card-text>
                                  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
                                </v-card-text>

                                <v-divider></v-divider>

                                <v-card-actions>
                                  <v-spacer></v-spacer>
                                  <v-btn
                                    color="primary"
                                    text
                                    @click="item.showEdit = false"
                                  >
                                    Save
                                  </v-btn>
                                </v-card-actions>
                              </v-card>
                            </v-dialog>
                          </div>
                        </v-list-item>
                      </v-card-text>
                    </div>
                  </v-expand-transition>
                </v-col>
              </v-row>
            </v-container>
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
          complete: false,
          showPanel: false,
          showEdit: false
        },
        {
          name: 'bread',
          price: 1.00,
          owner: ["Steven"],
          priority: "medium",
          complete: false,
          showPanel: false,
          showEdit: false
        },
        {
          name: 'coffee',
          price: 1.75,
          owner: ["Lyn"],
          priority: "high",
          complete: false,
          showPanel: false,
          showEdit: false
        },
        {
          name: 'vodka',
          price: 18.00,
          owner: ["Steven", "Lyn"],
          priority: "low",
          complete: false,
          showPanel: false,
          showEdit: false
        },
      ],
      newItemName: "",
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
        complete: false,
        showPanel: false,
        showEdit: false
      };
      this.shoppingList.push(newItem)
      console.log(newItem)
    },
    removeItem: function(index) {
      this.shoppingList.splice(index,1)
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
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
padding: 5px;
}
</style>

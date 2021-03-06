# VSnackbarQueue
>Simple plugin for queueing v-snackbars in Vuetify
* Extends VSnackbar component and adds items[] prop
* Queues Snackbars displaying one at a time 

### Plugin Usage
>Import as plugin in your main.js file

```text
//main.js
import Vue from 'vue'
import VuetifySnackbarQueue from 'vuetify-snackbar-queue'

Vue.use(VuetifySnackbarQueue)
```

### Example

```vue
<template>
      <v-container fluid>
        <v-row>
          <v-col cols="2">
            <v-btn color="primary" @click="addItem">Add to Queue</v-btn>
          </v-col>
        </v-row>
        <VSnackbarQueue :items="items" top right @remove="removeItem"></VSnackbarQueue>
      </v-container>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    items: [],
    colors: ["warning", "error", "info", "success"]
  }),
  methods: {
    addItem() {
      const vm = this;
      const index = vm.randomInt(0, vm.colors.length - 1);
      vm.items.push({
        id: vm.uniqueId("item_"),
        color: vm.colors[index],
        message: "This is an example"
      });
    },
    removeItem(id) {
      const vm = this;
      const index = vm.items.findIndex(item => item.id === id);

      if (index !== -1) {
        vm.items.splice(index, 1);
      }
    },
    randomInt(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    uniqueId: prefix =>
      `${prefix}_` +
      Math.random()
        .toString(36)
        .substr(2, 9)
  }
};
</script>
```

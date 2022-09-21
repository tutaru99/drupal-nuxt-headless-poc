<template>
  <v-container>
    <h3>might need a condition to stop nav recursion</h3>
    <NavigationMenu v-for="node in drupalHeaderData.items" :key="node.id" :node="node" />
    <ParentComponent />
  </v-container>
</template>


<script>
import axios from "axios";
export default {
  data() {
    return {
      drupalHeaderData: {},
    };
  },
  methods: {
    getHeader() {
      axios
        .get("https://headless.drupal.dk/?format=json&region=header")
        .then((response) => {
          this.drupalHeaderData = response.data;
          console.log("header", this.drupalHeaderData);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  mounted() {
    this.getHeader();
  },
};
</script>

<style lang="scss">
h3 {
  color: red;
}
</style>
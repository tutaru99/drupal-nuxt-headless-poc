<template>
  <div :class="['layout-block-navigation--' + drupalHeaderData.menu_name]">
    <NavigationMenuItem v-for="node in drupalHeaderData.items" :key="node.id" :node="node" />
  </div>
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

<style lang="scss" scoped>

</style>
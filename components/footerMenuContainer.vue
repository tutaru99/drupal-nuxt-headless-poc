<template>
  <div :class="['layout-block-footer--' + drupalFooterData.menu_name]">
    <FooterMenuItem v-for="node in drupalFooterData.items" :key="node.id" :node="node" />
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      drupalFooterData: {},
    };
  },
  methods: {
    getFooter() {
      axios
        .get("https://headless.drupal.dk/?format=json&region=footer")
        .then((response) => {
          this.drupalFooterData = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  mounted() {
    this.getFooter();
  },
};
</script>

<style lang="scss" scoped>

</style>
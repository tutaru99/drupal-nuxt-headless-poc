<template>
  <div :class="['layout-block--' + data.bundle]">
    <h3>RTE Component</h3>
    <div v-html="data.field_text"></div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
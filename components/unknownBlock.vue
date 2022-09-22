<template>
  <div :class="['layout-block--' + data.bundle]">
    <v-divider></v-divider>
    <h3>Unknown Block</h3>
    {{ data.bundle }} <br>
    {{ data }}
    <v-divider></v-divider>
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
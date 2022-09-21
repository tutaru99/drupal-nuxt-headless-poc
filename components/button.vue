<template>
  <div :class="['layout-block--' + data.bundle]">
    <h3>Button Component</h3>
    <nuxt-link :to="data.field_button.url">
      <v-btn color="primary purple px-15" dark>{{ data.field_button.title}}</v-btn>
    </nuxt-link>
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
    mounted() {
    },
  };
</script>

<style lang="scss" scoped>

</style>
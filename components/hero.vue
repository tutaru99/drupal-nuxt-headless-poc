<template>
  <div :class="['layout-block--' + data.bundle]">
    <h3>Hero Component</h3>
    <p>{{ data }}</p>
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
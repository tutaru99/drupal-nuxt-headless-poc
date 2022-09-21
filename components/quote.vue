<template>
  <div :class="['layout-block--' + data.bundle]">
  <h3>Quote Component</h3>
  <h1>"{{ data.field_quote_text }}"</h1>
  <h4 class="pl-5">-{{ data.field_quote_source }}</h4>
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
<template>
  <div :class="['layout-block--' + data.bundle]">
    <!-- if link starts with http -->
    <a
      v-if="data.field_button.url.startsWith('http')"
      :href="data.field_button.url"
      target="_blank"
      :class="['button' + ' ' + data.field_button.class + ' ' + 'button--' + data.field_button_alignment]">
      {{ data.field_button.title }}
    </a>

    <!-- Internal link -->
    <nuxt-link
      v-else
      :to="data.field_button.url"
      :href="data.field_button.url"
      :class="['button' + ' ' + data.field_button.class + ' ' + 'button--' + data.field_button_alignment]">
      {{ data.field_button.title }}
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
};
</script>

<style lang="scss" scoped>
  .layout-block--button {
    .button {
      position: relative;
      display: inline-flex;
      text-decoration: none;
      background-color: #C9013E;
      color: #fff;
      padding: 10px 20px;
      text-transform: uppercase;
      font-weight: 700;
      font-size: 14px;
      letter-spacing: 1px;
      margin: 0;
      border: 0;
      box-shadow: none;
      transition: all 0.3s ease-in-out;
      border-radius: 15px;

      &:hover {
        background-color: #fff;
        color: #000;
      }

      &--left {
        float: left;
      }

      &--center {
        left: 50%;
        transform: translateX(-50%);

      }

      &--right {
        float: right;
      }

      &--ghost {
        background-color: transparent;
        color: #fff;
        border: 1px solid #C9013E;
        border-radius: 15px;

        &:hover {
          background-color: #C9013E;
          color: #fff;
        }
      }
    }
  }
</style>
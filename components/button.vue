<template>
  <div :class="['layout-block--' + data.bundle]">
    <h3>Button Component</h3>

    <!-- if link starts with http -->
    <a
      v-if="data.field_button.url.startsWith('http')"
      :href="data.field_button.url"
      target="_blank"
      :class="['button' + ' ' + data.field_button.class + ' ' + 'button--' + data.field_button_alignment]">
      <v-btn>{{ data.field_button.title }}</v-btn>
    </a>

    <!-- Internal link -->
    <nuxt-link
      v-else
      :to="data.field_button.url"
      :href="data.field_button.url"
      :class="['button' + ' ' + data.field_button.class + ' ' + 'button--' + data.field_button_alignment]">
      <v-btn>{{ data.field_button.title }}</v-btn>
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
    console.log("button data", this.data);
  },
};
</script>

<style lang="scss" scoped>
  .layout-block--button {
    a {
      text-decoration: none;
    }
    .button {
      & .v-btn {
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
      }

      &--left {
        float: left;
      }

      &--right {
        float: right;
      }

      &--ghost {
        & .v-btn {
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
  }
</style>
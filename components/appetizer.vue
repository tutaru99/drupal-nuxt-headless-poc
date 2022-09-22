<template>
  <div :class="['layout-block--' + data.bundle]">
    <h3>Appetizer Component</h3>
    <h1>{{ data.field_appetizer_headline }}</h1>
    <br />
    <div v-html="data.field_appetizer_text"></div>
    <br />
    {{ data.field_appetizer_cta }} - (figure out btn target=blank)<br />
    <nuxt-link :to="data.field_appetizer_cta.url" target="_blank">
      <v-btn color="primary purple px-15" dark>{{
        data.field_appetizer_cta.title
      }}</v-btn>
    </nuxt-link>
    <br />
    text position - {{ data.field_appetizer_text_alignment }}

    <picture>
      <div
        v-for="el in data.field_appetizer_image.field_media_image.sources"
        :key="el.id"
      >
        <source
          v-if="el.media"
          :media="el.media"
          :srcset="`https://headless.drupal.dk${el.srcset}`"
        />
      </div>
      <img
        v-bind:src="
          'https://headless.drupal.dk' +
          data.field_appetizer_image.field_media_image.img_element.uri
        "
        @error="handleBrokenImageError"
      />
    </picture>
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
  methods: {
    handleBrokenImageError(e) {
      e.target.src =
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ0fMuDbBXXy2LT_ag2brlniXW_yxy_UFYdkw&usqp=CAU";
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
<template>
  <div :class="['layout-block--' + data.bundle]">
    <h3>Hero Component</h3>
    <div v-html="data.field_hero.field_text"></div>

    <p>text position{{ data.field_hero.field_text_position }}</p>
    <p>{{ data.field_hero.field_cta }}</p>

    <NuxtLink :to="`${data.field_hero.field_cta.url}`">
      <v-btn color="primary purple px-15" dark>{{
        data.field_hero.field_cta.title
      }}</v-btn>
    </NuxtLink>

    <picture>
      <div
        v-for="el in data.field_hero.field_background.field_media_image.sources"
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
          data.field_hero.field_background.field_media_image.img_element.uri
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
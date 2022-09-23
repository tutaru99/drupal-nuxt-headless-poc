<template>
  <div :class="['layout-block--' + data.bundle]">
    <h3 class="text-center">Articles Component</h3>
    <div class="d-flex">
      <v-row>
        <v-card
          v-for="article in data.field_articles.entities"
          :key="article.id"
          class="ma-3"
          max-width="400"
        >
          <v-img
            :src="
              'https://headless.drupal.dk' +
              article.field_list_media.field_media_image.img_element.uri
            "
            height="200px"
          ></v-img>

          <v-card-title>{{ article.title }}</v-card-title>

          <v-card-text>
            <p>{{ article.field_description }}</p>
          </v-card-text>

          <NuxtLink :to="`${article.url}`"> Go to article </NuxtLink>
        </v-card>
      </v-row>
    </div>
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
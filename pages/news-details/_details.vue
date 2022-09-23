<template>
  <div>
    <h1 class="text-center pa-3">News Details</h1>
    <v-card class="mx-auto pa-5" max-width="444">
      <v-card-text>
        <div class="pa-2">
          id - <span class="titlexd">{{ singleNew.id }}</span>
        </div>
        <!-- <p class="pa-2 text-h4 titlexd">{{ singleNew.title }}</p> -->
        <div v-if="imageBlock.length > 0">
          <v-img :src="`https://headless.drupal.dk/${imageBlock}`"></v-img>
          IMAGE FROM DRUPAL News Details block BLOCK! Woohoo!
        </div>
        <p class="pa-2 text-h4 titlexd">{{ singleNew.field_description }}</p>
        <p class="pa-2">
          <!-- completed - <span class="titlexd">{{ singleNew.completed }}</span> -->
        </p>
        <div class="text--primary"></div>
      </v-card-text>
      <v-card-actions>
        <v-btn color="purple" outlined to="/news">all news</v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  computed: {
    newsList() {
      return this.$store.state.news.storeNews;
    },
  },
  data() {
    return {
      singleNew: [],
      routeId: "",
      imageBlock: [],
    };
  },
  methods: {
    async getNews() {
      // get last part of url for the id
      this.routeId = this.$nuxt.$route.path.split("/").pop();

      if (this.$store.state.news.storeNews.length === 0) {
        // Make api call with the id
        axios
          .get(
            "https://headless.drupal.dk/node/" +
              this.routeId +
              "?format=json&region=content"
          )
          .then((response) => {
            this.singleNew = response.data;

            this.imageBlock =
              this.singleNew.layout_builder__layout[0].regions.content[2].field_image_media.field_media_image.sources[0].srcset;

            console.log(this.singleNew);
          })
          .catch((error) => {
            console.log(error);
          });
      } else {
        //  get the news from the store instead of the api
        this.singleNew = this.newsList[0].find(
          (item) => item.id == this.routeId
        );
      }
    },
  },
  mounted() {
    // this.getNews();
  },
};
</script>

<style lang="scss" scoped>
.titlexd {
  color: #42b983;
}
</style>
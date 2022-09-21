<template>
  <div>
    <h1>News Overview!</h1>
    <div class="wrapper d-flex">
      <v-card
        class="mx-auto pa-5 ma-5"
        v-for="singleNestedNews in nestedNews"
        :key="singleNestedNews.id"
        max-width="444"
      >
        <v-card-text>
          <div class="pa-2">
            <span class="titlexd">
              {{ singleNestedNews.id }}
              <v-img
                :src="`https://headless.drupal.dk/${singleNestedNews.field_list_media.field_media_image.sources[0].srcset}`"
              ></v-img>
            </span>
          </div>
          <p class="pa-2 text-h4 titlexd"></p>
          <p class="pa-2">
            <span class="titlexd">
              {{ singleNestedNews.url }}
            </span>
          </p>
          <div class="text--primary">
            {{ singleNestedNews.field_description }}
          </div>
        </v-card-text>
        <v-card-actions>
          <v-btn color="purple" outlined :to="'/news-details/' + singleNestedNews.id">Read More</v-btn>
        </v-card-actions>
      </v-card>
    </div>
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
      news: [],
      nestedNews: [],
    };
  },

  methods: {
    // async getNews() {
    //   if (this.$store.state.news.storeNews.length === 0) {
    //     axios
    //       .get("https://jsonplaceholder.typicode.com/todos/")
    //       .then((response) => {
    //         this.news = response.data;
    //         // send to json store Vuex
    //         this.$store.commit("news/addNews", this.news);
    //         console.log(this.news);
    //       })
    //       .catch((error) => {
    //         console.log(error);
    //       });
    //   } else {
    //     this.news = this.$store.state.news.storeNews;
    //   }
    // },

    async getNews() {
      axios
        .get("https://headless.drupal.dk/?format=json&region=content")
        .then((response) => {
          this.news = response.data;
          // send to json store Vuex
          // this.$store.commit("news/addNews", this.news);

          this.nestedNews = this.news.layout_builder__layout[0].regions.content[1].field_articles.entities;
          console.log(
            this.news.layout_builder__layout[0].regions.content[1]
              .field_articles.entities
          );
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },

  mounted() {
    this.getNews();
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  flex-wrap: wrap;
}
h1 {
  text-align: center;
}
.news-item {
  margin: 10px 0;
  text-decoration: none;

  a {
    color: #42b983;
    text-decoration: none;
    font-size: 24px;
  }
}
.titlexd {
  color: #42b983;
  font-size: 16px;
}
</style>
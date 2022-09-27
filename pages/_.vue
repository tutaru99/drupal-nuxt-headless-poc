<template>
  <div>
    <div v-for="item in feed.content" :key="item.id">
      <h1 v-if="item.field_hide_title === false">{{ item.label }}</h1>
      <div v-if="item.type === 'entity' && item.entity_type === 'node'">
        <Section
          v-if="item.bundle === 'page'"
          :data="item"
        />

        <Article
          v-else-if="item.bundle === 'article'"
          :data="item"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      feed: [],
    };
  },
  methods: {
    async getInitialData() {
      axios
        .get(`https://headless.drupal.dk${this.$route.path}?format=json`)
        .then((response) => {
          this.feed = response.data;
          console.log("article news feed", this.feed);
        })
        .catch((error) => {
          // console.log(error);
          // js alert
          if (error) {
            alert("No data found -> mount 404 component l8r. This component is responsible for 404 now.");
          } else {
            alert("Something went wrong");
          }
        });
    },
  },
  created() {
    this.getInitialData();
  },
};

</script>

<style lang="scss" scoped>
</style>
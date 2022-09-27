<template>
  <v-container>
    <v-row class="pb-5">
      <TheHeader />
    </v-row>
    <div v-for="item in someData.content" :key="item.id">
      <h1 v-if="item.field_hide_title === false">{{ item.label }}</h1>
      <div v-if="item.type === 'entity' && item.entity_type === 'node'">
      <Section
        v-if="item.bundle === 'page'"
        :data="item"
      />
      </div>
    </div>

    <!-- {{ someData.content?.[0] }} -->
      <TheFooter />
  </v-container>
</template>

<style lang="scss">
</style>

<script>
import axios from "axios";

export default {
    data() {
        return {
            someData: [],
        };
    },
    methods: {
        async getInitialData() {
            axios
                .get("https://headless.drupal.dk/?format=json")
                .then((response) => {
                this.someData = response.data;
                console.log("someData", this.someData);
            })
                .catch((error) => {
                console.log(error);
            });
        },
    },
    created() {
        this.getInitialData();
    },
};
</script>
<template>
  <v-container>
    <v-row no-gutters>
      <v-col cols="12" sm="12" md="12">
        <h1 class="text-center">Parent Component</h1>
        <div
          v-for="section in layoutBuilder"
          :key="section.id"
          :class="[
            'section',
            section.layout_id,
            'column-widths--' + section.layout_settings.column_widths,
            section.layout_settings.color_theme,
            'spacing-top--' + section.layout_settings.column_spacing_top,
            'spacing-bottom--' + section.layout_settings.column_spacing_bottom,
          ]"
        >
          <!-- {{ section.layout_id }} -->
          <div v-for="region in section.regions" class="col" :key="region.id">
            <!-- Dynamic classes constructor by @Soren on sections-->
            <div v-for="content in region" :key="content.id">
              <!-- <h1> {{ content.bundle }} - type of component (content/block types)</h1> -->

              <!-- if content.build is article  -->
              <Articles v-if="content.bundle === 'articles'" :data="content" />

              <!-- rte component -->
              <Rte v-else-if="content.bundle === 'rte'" :data="content" />

              <!-- quote component -->
              <Quote v-else-if="content.bundle === 'quote'" :data="content" />

              <!-- button component -->
              <Button v-else-if="content.bundle === 'button'" :data="content" />

              <!-- image component -->
              <imageComponent
                v-else-if="content.bundle === 'image'"
                :data="content"
              />

              <!-- hero component -->
              <Hero v-else-if="content.bundle === 'hero'" :data="content" />

              <!-- only if none other match -->
              <UnknownBlock v-else :data="content"></UnknownBlock>
            </div>
          </div>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      drupalData: [],
      layoutBuilder: [],
    };
  },
  methods: {
    async getDrupalData() {
      axios
        .get("https://headless.drupal.dk/?format=json&region=content")
        .then((response) => {
          this.drupalData = response.data;
          this.layoutBuilder = this.drupalData[0].layout_builder__layout;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  mounted() {
    this.getDrupalData();
  },
};
</script>

<style lang="scss">
h3 {
  color: red;
}
</style>
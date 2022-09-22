<template>
  <v-container class="text-center">
    <v-row no-gutters>
      <v-col cols="12" md="12">
        <h1 class="text-center">Parent Component</h1>
        <v-row
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
          <!-- {{section.layout_settings.column_widths}} -->

          <!-- TODO DEFINE ALL POSSBILE COL SELECTION OPTIONS for section
            67 - 33% HOW?!?!?!? mb on mounted trigger function and see what happens
            33 - 67%
          -->

          <v-col
            cols="12"
            :md="[
              (section.layout_settings.column_widths == '33-33-33' ? 4 : '')
                | (section.layout_settings.column_widths == '50-50' ? 6 : '')
                | (section.layout_settings.column_widths == '67-33' ? assignColumns8to4(8) : '')
                | (section.layout_settings.column_widths == '33-67' ? assignColumns4to4(4) : '') |
                (section.layout_settings.column_widths == '' ? 12 : ''),
            ]"
            sm="12"
            v-for="region in section.regions"
            :key="region.id"
          >
            <!-- Dynamic classes constructor by @Soren on sections-->
            <v-row>
              <v-col v-for="content in region" :key="content.id">
                <!-- <h1> {{ content.bundle }} - type of component (content/block types)</h1> -->

                <!-- if content.build is article  -->
                <Articles
                  v-if="content.bundle === 'articles'"
                  :data="content"
                />

                <!-- rte component -->
                <Rte v-else-if="content.bundle === 'rte'" :data="content" />

                <!-- quote component -->
                <Quote v-else-if="content.bundle === 'quote'" :data="content" />

                <!-- button component -->
                <Button
                  v-else-if="content.bundle === 'button'"
                  :data="content"
                />

                <!-- appetizer component -->
                <Appetizer
                  v-else-if="content.bundle === 'appetizer'"
                  :data="content"
                />

                <!-- image component -->
                <imageComponent
                  v-else-if="content.bundle === 'image'"
                  :data="content"
                />

                <!-- hero component -->
                <Hero v-else-if="content.bundle === 'hero'" :data="content" />

                <!-- only if none other match -->
                <UnknownBlock v-else :data="content"></UnknownBlock>
              </v-col>
            </v-row>
          </v-col>
        </v-row>
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
      unevenSection: null,
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

  computed: {
    assignColumns8to4() {
      // rotate between 4 and 8
      let previouValue = null;
      let newValue = null;
      return function (value) {
        if (previouValue === value) {
          newValue = value === 4 ? 8 : 4;
        } else {
          newValue = value;
        }
        previouValue = newValue;
        return newValue;
      };
    },

    assignColumns4to4() {
      // rotate between 8 and 4
      let previouValue = null;
      let newValue = null;
      return function (value) {
        if (previouValue === value) {
          newValue = value === 8 ? 4 : 8;
        } else {
          newValue = value;
        }
        previouValue = newValue;
        return newValue;
      };
    },

  },
};
</script>

<style lang="scss">
h3 {
  color: red;
}
</style>
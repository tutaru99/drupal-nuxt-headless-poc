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
            33 - 57%


          -->
          <v-col cols="12"
            :md="[(section.layout_settings.column_widths == '33-33-33' ? 4 : '') |
            (section.layout_settings.column_widths == '50-50' ? 6 : '') |
            // (section.layout_settings.column_widths == '67-33' ? this.doShit()  : '') |
            (section.layout_settings.column_widths == '' ? 12 : '')]"
            sm="12"
            v-for="region in section.regions"  :key="region.id">
            <!-- Dynamic classes constructor by @Soren on sections-->
            <v-row>
            <v-col v-for="content in region" :key="content.id">
              <!-- <h1> {{ content.bundle }} - type of component (content/block types)</h1> -->

              <!-- if content.build is article  -->
              <Articles v-if="content.bundle === 'articles'" :data="content" />

              <!-- rte component -->
              <Rte v-else-if="content.bundle === 'rte'" :data="content" />

              <!-- quote component -->
              <Quote v-else-if="content.bundle === 'quote'" :data="content" />

              <!-- button component -->
              <Button v-else-if="content.bundle === 'button'" :data="content" />

              <!-- appetizer component -->
              <Appetizer v-else-if="content.bundle === 'appetizer'" :data="content" />

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
import Appetizer from "./appetizer.vue";

export default {
    data() {
        return {
            drupalData: [],
            layoutBuilder: [],
            eightToFour: 8,
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
        doShit() {
            // initial value is 8, if hit again its 4
            return this.eightToFour = this.eightToFour == 8 ? 4 : 8;
        },
    },
    mounted() {
        this.getDrupalData();
    },
    components: { Appetizer }
};
</script>

<style lang="scss">
h3 {
  color: red;
}
</style>
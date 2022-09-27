<template>
  <v-container>
    <v-row no-gutters>
      <v-col cols="12" md="12">
        <v-row
          v-for="section in layoutBuilder"
          :key="section.id"
          :class="[
            'section',
            section.layout_id,
            'column-widths--' + section.layout_settings.column_widths,
            section.layout_settings.color_theme,
            section.layout_settings.column_spacing_top,
            section.layout_settings.column_spacing_bottom,
          ]"
        >
          <v-col
            cols="12"
            :md="assignMdCollumnsHandler(section.layout_settings.column_widths)"
            sm="12"
            v-for="region in section.regions"
            :key="region.id"
          >
            <!-- Dynamic classes constructor by @Soren on sections-->
            <v-row>
              <v-col v-for="content in region" :key="content.id">

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

                <!-- hero component -->
                <!-- <Video v-else-if="content.bundle === 'video'" :data="content" /> -->

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
  props: {
    md: {
      type: Array | Object,
      default: () => ({}),
    },
  },
  data() {
    return {
      drupalData: [],
      layoutBuilder: [],
      unevenSection: null,
    };
  },
  methods: {
    assignMdCollumnsHandler(colValue) {
      if (colValue == "33-33-33") {
        return 4;
      } else if (colValue == "50-50") {
        return 6;
      } else if (colValue == "67-33") {
        return this.assignColumns8to4(8);
      } else if (colValue == "33-67") {
        return this.assignColumns4to8(4);
      } else if (colValue == "") {
        return 12;
      }
    },

    async getDrupalData() {
      axios
      .get(`https://headless.drupal.dk${this.$route.path}?format=json&region=content`)
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

    assignColumns4to8() {
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

.section {
  &--spacing-top {
    &-large {
      padding-top: 6rem;
    }

    &-medium {
      padding-top: 4rem;
    }

    &-small {
      padding-top: 2rem;
    }
  }

  &--spacing-bottom {
    &-large {
      padding-bottom: 6rem;
    }

    &-medium {
      padding-bottom: 4rem;
    }

    &-small {
      padding-bottom: 2rem;
    }
  }
}
</style>
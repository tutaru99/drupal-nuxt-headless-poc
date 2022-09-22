<template>
  <div>
    <h3>Video comp</h3>

    <h2>{{ data.field_video_headline }}</h2>
    <h2>{{ data.field_video_subline }}</h2>
    <div v-html="data.field_video_media.field_media_oembed_video.html"></div>
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
  mounted() {
    console.log(this.data);
  },
};
</script>

<style lang="scss" scoped>
</style>
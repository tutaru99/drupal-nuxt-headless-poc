<template>
  <div>
    <ul>
      <li>
        <nuxt-link color="#C9013E" :to="node?.url">{{ node?.title }}</nuxt-link>
      </li>
      <div v-if="hasChildren">
        <NavigationMenuItem
          v-for="child in node?.below"
          :key="child.id"
          :node="child"
        />
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    node: {
      type: Object,
      required: false,
    },
  },

  computed: {
    hasChildren() {
      const { below } = this.node;

      if (below.length == 0) {
        return false;
      } else if (!below.length) {
        return true;
      } else {
        return;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
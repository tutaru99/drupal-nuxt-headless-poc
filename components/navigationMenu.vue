<template>
  <div>
    <ul>
      <li>
        <span class="purple"> {{ node?.title }}</span> -
        <span class="blue">{{ node?.url }}</span>
      </li>
      <div v-if="hasChildren">
        <navigationMenu
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
        console.log('no children - is empty', below);
        return false;
      }
      else if (!below.length) {
        console.log('has children', below);
        return true;
      }
      else {
        console.log('shouldnt be ever hit')
        return;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
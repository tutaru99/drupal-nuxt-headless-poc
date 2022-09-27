<template>
  <div>
    <ul>
      <li>
        <a v-if="node?.url.startsWith('http')" :href="node?.url" class="navigation-item">{{ node?.title }}</a>
        <nuxt-link v-else :to="node?.url" class="navigation-item">{{ node?.title }}</nuxt-link>
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
  ul li {
    padding: 5px;
  }
  .navigation-item {
    text-decoration: none;
    color: #fff;
    font-weight: 700;
    text-transform: uppercase;
    padding: 10px 20px;
    transition: all 0.2s ease-in-out;
    border-radius: 15px;

    &:hover {
      background-color: #C9013E;;
      color: #fff;
      border-radius: 15px;
    }
  }
  .nuxt-link-active {
    color: #C9013E;
  }
</style>
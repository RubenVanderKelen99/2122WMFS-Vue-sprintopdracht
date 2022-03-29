<template>
  <ul>
    <li v-for="w in works" :key="w.key">
      <LibTeaser :work="w"/>
    </li>
  </ul>
</template>

<script>
import LibTeaser from "../molecules/LibTeaser.vue";
export default {
  components: { LibTeaser },
  props: {
    works: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped lang="scss">
ul {
  padding: 0;
  margin: 0;
  list-style: none;
}

.selected {
  background-color: var(--color);
  color: var(--color-background);
}
</style>

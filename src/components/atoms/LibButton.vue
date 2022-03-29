<template>
  <button>
    <slot />
  </button>
</template>

<script>
export default {
  emits: ["subjectSelected"],
  methods: {
    subjectSelected(subject) {
      this.$emit("subjectSelected", `${subject}`);
    },
  },
};
</script>

<style scoped lang="scss">
.button {
  border-bottom: 1px solid;
  padding: 0.3em 0.8em;
  line-height: 1;
  box-shadow: none;

  &:hover,
  &:focus-visible {
  }
}
</style>

<template>
  <div class="teaser">
    <h3>{{ work.title }}</h3>
    <h4 v-for="a in work.authors" :key=a.key>{{ a.name }}</h4>
    <li v-for="s in work.subject.slice(3)" :key="s.value">
      <LibButton :subject="w">{{ s.value }}</LibButton>
    </li>
  </div>
</template>

<script>
import LibButton from "../atoms/LibButton.vue";

export default {
  components: { LibButton },
  props: {
    work: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped lang="scss">
.teaser {
  border-bottom: 1px solid;
  padding: 1rem;

  > * {
    margin-bottom: 1rem;
  }

  .subjects {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5em;
  }
}
</style>

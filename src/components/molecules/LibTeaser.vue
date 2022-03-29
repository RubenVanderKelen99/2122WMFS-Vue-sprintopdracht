<template>
  <div class="teaser">
    <h3>{{ work.title }}</h3>
    <div class="authors">
      <h4 v-for="a in work.authors" :key="a.key">{{ a.name }}</h4>
    </div>
    <div class="subjects">
      <LibButton
        v-for="s in work.subject.slice(0, 3)"
        :key="s"
        :subject="s"
        @click="$emit('subjectSelected', s)"
      >
        {{ s }}
      </LibButton>
    </div>
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

  .authors {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 0.5em;
  }

  .subjects {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 0.5em;
  }
}
</style>

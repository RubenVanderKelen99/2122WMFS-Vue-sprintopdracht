<script>
import LibList from "./components/organisms/LibList.vue";
import LibDetail from "./components/organisms/LibDetail.vue";
export default {
  components: { LibDetail, LibList },
  data() {
    return {
      work_count: "",
      works: "",
      subject: "",
      key: "",
      loading: false,
      error: "",
    };
  },
  computed: {
    urlList() {
      let url = "";
      url += "https://openlibrary.org/subjects/";
      url += this.subject;
      url += ".json";
      return encodeURI(url);
    },
    urlDetail() {
      let url = "";
      url += "https://openlibrary.org";
      url += this.key;
      url += ".json";
      return encodeURI(url);
    },
  },
  methods: {
    fetchList(arg) {
      this.loading = true;
      this.subject = arg;
      fetch(this.urlList)
        .then((res) => res.json())
        .then((res) => {
          this.work_count = res.work_count;
          this.works = res.works;
          this.loading = false;
        })
        .catch((error) => {
          this.error = error;
          this.loading = false;
        });
    },
    /*fetchDetail(arg) {
      this.loading = true;
      this.key = arg;
      fetch(this.urlDetail)
        .then((res) => res.json())
        .then((res) => {
          this.loading = false;
          ...
        })
        .catch((error) => {
          this.error = error;
          this.loading = false;
        });
    },*/
  },
  mounted() {
    this.fetchList("computers");
  },
};
</script>

<template>
  <header>
    <h1>The little libre library</h1>
  </header>
  <main>
    <div>
      <h2 class="visually-hidden">Results</h2>
      <LibList v-if="works?.length > 0" :works="works" />
      <p v-else-if="error" class="error">
        Geen resultaten gevonden...<br />(● ︵ ●)
      </p>
    </div>
    <div class="detail">
      <LibDetail />
    </div>
    <div v-if="loading" class="loading">...loading</div>
  </main>
</template>

<style scoped lang="scss">
@import "./assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  font-weight: normal;
}

main {
  display: flex;

  > .detail {
    padding: 0 2rem 2rem;
  }

  > * {
    flex: 1 1 50%;
  }

  .loading {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    text-shadow: 0 0 2px black, 0 0 2px black, 0 0 2px black, 0 0 2px black;
  }
}

.visually-hidden {
  clip-path: inset(50%);
  height: 1px;
  overflow: hidden;
  position: absolute;
  white-space: nowrap;
  width: 1px;
}

.sticky {
  position: sticky;
  top: 0;
}
</style>

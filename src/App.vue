<template>
  <div id="app">
    <MoviesLoader />
    <NotificationMessage />
    <PosterBackground :poster="posterBackground" />
    <HeaderNavigation />
    <MoviesList :list="moviesList" @changePoster="onChangePoster" />
    <MoviesPagination
      :current-page="currentPage"
      :per-page="moviesPerPage"
      :total="moviesLength"
      @changedPage="onChangedPage"
    />
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import MoviesList from "./components/MoviesList.vue";
import PosterBackground from "./components/PosterBackground.vue";
import MoviesPagination from "./components/MoviesPagination.vue";
import MoviesLoader from "./components/MoviesLoader.vue";
import HeaderNavigation from "./components/HeaderNavigation.vue";
import NotificationMessage from "./components/NotificationMessage.vue";

export default {
  name: "App",
  components: {
    MoviesList,
    PosterBackground,
    MoviesPagination,
    MoviesLoader,
    HeaderNavigation,
    NotificationMessage,
  },
  data: () => ({
    posterBackground: "",
  }),
  computed: {
    ...mapGetters("movies", [
      "moviesList",
      "currentPage",
      "moviesPerPage",
      "moviesLength",
    ]),
  },
  methods: {
    ...mapActions("movies", ["changeCurrentPage"]),
    onChangePoster(poster) {
      this.posterBackground = poster;
    },
    onChangedPage(page) {
      this.$router.push({ query: { page } });
    },
    onPageQueryChange({ page = 1 }) {
      this.changeCurrentPage(Number(page));
    },
  },
  watch: {
    "$route.query": {
      handler: "onPageQueryChange",
      immediate: true,
      deep: true,
    },
  },
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
</style>

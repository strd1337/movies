<template>
  <header class="header">
    <BNavbar class="navbar" type="light" variant="light">
      <BContainer>
        <BNavbarBrand href="#" class="navbar-brand">MovieDB</BNavbarBrand>
        <BNavForm>
          <BFormInput
            class="mr-sm-2 search-input"
            placeholder="Search"
            debounce="500"
            v-model="searchValue"
          ></BFormInput>
        </BNavForm>
      </BContainer>
    </BNavbar>
  </header>
</template>

<script>
import { mapActions } from "vuex";

export default {
  name: "HeaderNavigation",
  data: () => ({
    searchValue: "",
  }),
  watch: {
    searchValue: "onSearchValueChanged",
  },
  methods: {
    ...mapActions("movies", [
      "searchMovies",
      "fetchMovies",
      "toggleSearchState",
    ]),
    onSearchValueChanged(value) {
      if (value) {
        this.searchMovies(value);
        this.toggleSearchState(true);
      } else {
        this.fetchMovies();
        this.toggleSearchState(false);
      }
    },
  },
};
</script>

<style scoped>
.header {
  margin-bottom: 30px;
}

.navbar {
  background-color: rgba(0, 0, 0, 0.7) !important;
}

.navbar-brand {
  color: white !important;
}

.search-input {
  color: white;
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(0, 0, 0, 0.6);
}

.search-input:focus {
  box-shadow: none;
  color: white;
  background: rgba(255, 255, 255, 0.2);
  border-color: rgba(0, 0, 0, 0.6);
}
</style>

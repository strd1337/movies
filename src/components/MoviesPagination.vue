<template>
  <div class="movies-pagination d-flex justify-content-center">
    <BPagination
      v-model="currentPageModel"
      :per-page="perPage"
      :total-rows="total"
    >
    </BPagination>
  </div>
</template>

<script>
export default {
  name: "MoviesPagination",
  props: {
    currentPage: {
      type: Number,
      default: 1,
    },
    total: {
      type: Number,
      default: 1,
    },
    perPage: {
      type: Number,
      default: 1,
    },
  },
  computed: {
    currentPageModel: {
      get() {
        return this.currentPage;
      },
      set(value) {
        this.$emit("changedPage", value);
      },
    },
  },
};
</script>

<style scoped>
.movies-pagination {
  margin-top: auto;
}

.movies-pagination >>> .pagination .page-item .page-link {
  background-color: transparent;
  font-size: 12px;
  color: white;
  box-shadow: none;
}

.movies-pagination >>> .pagination .page-item.active .page-link {
  border-color: white;
  background-color: white;
  color: black;
}

.movies-pagination >>> .pagination .page-item.disabled .page-link {
  color: gray;
}
</style>

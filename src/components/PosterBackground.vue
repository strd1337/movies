<template>
  <div class="poster-page-background" :style="posterStyle"></div>
</template>

<script>
export default {
  name: "PosterBackground",
  props: {
    poster: {
      type: String,
      default: "",
    },
  },
  data: () => ({
    defaultPosterBackground:
      "background-image: linear-gradient(45deg,rgb(0, 3, 38) 0%, rgb(82, 15, 117) 100%);",
  }),
  computed: {
    posterStyle() {
      return {
        "background-image": this.posterBackground,
      };
    },
    posterBackground() {
      return this.poster ? `url(${this.poster})` : this.defaultPosterBackground;
    },
  },
};
</script>

<style scoped>
.poster-page-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: -1;
  background-image: linear-gradient(
    45deg,
    rgb(16, 23, 14) 0%,
    rgb(29, 105, 124) 100%
  );
  background-size: cover;
  background-position: center;
  transition: all 0.2s ease;
}

.poster-page-background::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: linear-gradient(
    45deg,
    rgb(16, 23, 14) 0%,
    rgb(29, 105, 124) 100%
  );
  opacity: 0.7;
}
</style>

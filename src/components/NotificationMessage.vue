<template>
  <div></div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "NotificationMessage",
  computed: {
    ...mapGetters(["messagePool"]),
  },
  watch: {
    messagePool: "showNotification",
  },
  methods: {
    showNotification({ message, title, variant }) {
      this.$root.$bvToast.toast(message, {
        title: title,
        variant: variant,
        solid: true,
        autohide: false,
        "no-auto-hide": true,
      });
    },
  },
};
</script>

<style scoped></style>

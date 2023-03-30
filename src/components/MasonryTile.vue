<template>
  <li class="masonry__image-wrapper">
    <img :src="image" class="masonry__image" loading="lazy" alt="demo image" />
  </li>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "MasonryTile",
  props: {
    image: {
      type: String,
      default: "",
    },
    tileIndex: {
      type: Number,
      default: null,
    },
  },
  setup() {
    return {};
  },
});
</script>

<style lang="scss" scoped>
@import "@/assets/scss/masonry.scss";
</style>

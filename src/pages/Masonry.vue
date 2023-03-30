<template>
  <section class="section">
    <ul class="masonry">
      <MasonryTile
        v-for="(image, index) in images"
        :key="image + index"
        :image="image"
        :tileIndex="index"
      />
    </ul>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { imagesConst } from "@/constants/common";
import MasonryTile from "@/components/MasonryTile.vue";

export default defineComponent({
  name: "Masonry",
  components: { MasonryTile },
  props: {
    displayWidth: {
      type: Number,
      default: 0,
    },
  },
  setup() {
    const images = imagesConst;
    return { images };
  },
});
</script>

<style lang="scss" scoped>
@import "@/assets/scss/masonry.scss";
</style>

<template>
  <main ref="mainRef">
    <Masonry />
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Masonry from "@/pages/Masonry.vue";

export default defineComponent({
  name: "App",
  components: { Masonry },
});
</script>

<style lang="scss">
@import "@/assets/scss/main.scss";
</style>

<template>
  <main ref="mainRef">
    <Masonry :displayWidth="displayWidth" />
  </main>
</template>

<script lang="ts">
import { defineComponent, onBeforeUnmount, onMounted, ref } from "vue";
import Masonry from "@/pages/Masonry.vue";

export default defineComponent({
  name: "App",
  components: { Masonry },
  setup() {
    const displayWidth = ref(0);
    const myObserver = new ResizeObserver((entries) => {
      entries.forEach((entry) => {
        displayWidth.value = entry.contentRect.width;
      });
    });

    onMounted(() => {
      myObserver.observe(mainRef.value);
    });

    onBeforeUnmount(() => {
      myObserver.disconnect();
    });

    const mainRef: any = ref(null);
    return { mainRef, displayWidth };
  },
});
</script>

<style lang="scss">
@import "@/assets/scss/main.scss";
</style>

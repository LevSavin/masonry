<template>
  <section class="section">
    <ul class="masonry">
      <MasonryTile
        v-for="(image, index) in imagesSource"
        :key="image + index"
        :image="image"
        :tileIndex="index"
      />
    </ul>
  </section>
</template>

<script lang="ts">
import { defineComponent, onBeforeMount, ref } from "vue";
import type { Ref } from "vue";
import { imagesConst } from "@/constants/common";
import MasonryTile from "@/components/MasonryTile.vue";

const rowTemplates = Object.freeze([
  {
    variant: "tallRow",
    count: 4,
    items: [],
    reverse: false,
  },
  {
    variant: "defaultRow",
    count: 2,
    items: [],
    reverse: false,
  },
]);

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
    const imagesSource = ref(imagesConst);
    const rows: Ref<any[]> = ref([]);

    const setRows = (rowTemplate = rowTemplates) => {
      const result: any = [];
      const src = imagesSource.value;
      // переменные для цикла
      let lastIndex = rowTemplate[0].count;
      let rowVariantIndex = 0;
      let count = rowTemplate[rowVariantIndex].count;

      for (let firstIndex = 0; firstIndex < src.length; null) {
        firstIndex = firstIndex + count;
        result.push(rowTemplate[rowVariantIndex]);

        // переключаем переменные для цикла
        if (rowVariantIndex + 1 < rowTemplate.length) {
          lastIndex = rowTemplate[rowVariantIndex].count;
          count = rowTemplate[rowVariantIndex].count;
          ++rowVariantIndex;
        } else {
          lastIndex = rowTemplate[0].count;
          count = rowTemplate[0].count;
          rowVariantIndex = 0;
        }

        // формируем массив
        const imagesArray = src.slice(firstIndex, lastIndex);
        console.log(firstIndex, lastIndex);
        result[result.length - 1].items.push(...imagesArray);
        lastIndex += rowTemplate[rowVariantIndex].count;
        //result.push(src.slice(firstIndex, lastIndex));
      }
      console.log(result);
      //rows.value.push({});
    };

    onBeforeMount(() => {
      //setRows();
    });

    return { imagesSource, rows };
  },
});
</script>

<style lang="scss" scoped>
@import "@/assets/scss/masonry.scss";
</style>

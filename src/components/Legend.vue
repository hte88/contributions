<template>
  <div
    v-for="(background, index) in color"
    :key="index"
    :style="{ 'background-color': background.color }"
    :title="background.min + ' >= ' + background.max"
    class="relative h-5 w-5 border m-0.5 z-0 cursor-pointer"
  ></div>
</template>

<script>
export default {
  props: {
    color: {
      Type: Object,
      default: () => [
        { min: 0, max: 0, color: "#ededed" },
        { min: 1, max: 9, color: "#acd6f2" },
        { min: 10, max: 19, color: "#7fa8c9" },
        { min: 20, max: 29, color: "#527ba0" },
        { min: 30, max: 10000, color: "#264e77" },
      ],
    },
  },
};
</script>

<style></style>

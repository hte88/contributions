<template>
    <ul class="squares">
      <li
        v-for="(day, index) in data"
        :key="index"
        :style="{
          'background-color': getColor(day.contribution),
        }"
        :title="day.contribution"
        class="relative h-5 w-5 border m-0.5 cursor-pointer font-medium items-center flex justify-center text-white text-xs transition delay-150 duration-300 ease-in-out transform hover:scale-125"
      >
        <div v-if="visibleContribution">{{ day.contribution }}</div>
      </li>
    </ul>
</template>
<script>
export default {
  props: {
    data: { Type: Object },
    visibleContribution: { Type: Boolean, default: false },
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
  methods: {
    getColor(contributionCount) {
      let background = null;
      for (const key in this.color) {
        if (
          contributionCount >= this.color[key].min &&
          contributionCount <= this.color[key].max
        ) {
          background = this.color[key].color;
        }
      }
      if (background === null) background = "#eeeeee";
      return background;
    },
  },
};
</script>

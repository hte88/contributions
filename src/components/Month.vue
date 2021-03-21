<template>
  <ul class="grid grid-flow-col gap-1 col-start-2 text-center">
    <li v-for="(month, index) in getMonthsList" :key="index">{{ month }}</li>
  </ul>
</template>
<script>
import dayjs from "dayjs";
export default {
  props: {
    minDate: {
      Type: String,
    },
    diffDays: {
      Type: Number,
    },
  },
  computed: {
    getMonthsList() {
      let monthTemp = dayjs(this.minDate).format("MMM");
      const monthsList = [monthTemp];
      for (let index = 0; index < this.diffDays; index++) {
        let monthOfYear = dayjs(this.minDate).add(index, "day").format("MMM");
        if (monthTemp !== monthOfYear) {
          monthsList.push(monthOfYear);
          monthTemp = monthOfYear;
        }
      }
      return monthsList;
    },
  },
};
</script>

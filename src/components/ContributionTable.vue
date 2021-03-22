<template>
  <div class="bg-white mt-10 py-10 px-5 overflow-x-auto">
    <div class="flex">
      <div class="inline-grid gap-2">
        <MonthsList :min-date="minDate" :diff-days="diffDays"></MonthsList>
        <WeekDay></WeekDay>
        <DaySquareList
          :data="newDataJson"
          :color="color"
          :visible-contribution="visibleContribution"
        ></DaySquareList>
      </div>
    </div>
    <div class="mt-10 mx-10 justify-between flex">
      <div class="flex flex-wrap">
        <Legend :color="color"></Legend>
      </div>
      <div>
        <button
          @click="visibleContribution = !visibleContribution"
          class="rounded bg-green-500 hover:bg-green-700 text-white px-4 py-2 focus:outline-none"
        >
          <span v-if="!visibleContribution">Show Contributions</span>
          <span v-else>Hide Contributions</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import dayjs from "dayjs";
import DaySquareList from "./DaySquareList.vue";
import WeekDay from "./WeekDay.vue";
import MonthsList from "./Month.vue";
import Legend from "./Legend.vue";
export default {
  props: {
    dataJson: { Type: Object, Required: true },
    color: { Type: Object },
  },
  data() {
    return {
      newDataJson: [],
      months: [],
      minDate: null,
      diffDays: null,
      visibleContribution: false,
    };
  },
  created() {
    this.init();
  },
  components: { DaySquareList, WeekDay, MonthsList, Legend },
  methods: {
    init() {
      const dataJson = this.dataJson;
      const dates = Object.keys(dataJson);
      const sortedDates = dates.sort();
      const minDate = this.getMinDate(sortedDates);
      const minSunday = this.getSunday(minDate);
      this.minDate = minSunday;
      const maxDate = this.getMaxDate(sortedDates);
      const diffDays = this.getDiffDays(minSunday, maxDate);
      this.diffDays = diffDays;
      this.newDataJson = this.completedDataJson(minSunday, diffDays);
    },
    getMinDate(sortedDates) {
      return sortedDates[0];
    },
    getMaxDate(sortedDates) {
      const lastDate = sortedDates.length - 1;
      return sortedDates[lastDate];
    },
    getDiffDays(minDate, maxDate) {
      const diffTime = Math.abs(new Date(maxDate) - new Date(minDate));
      const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
      return diffDays;
    },
    completedDataJson(minDate, diffDays) {
      const dates = [];
      for (let index = 0; index < diffDays + 1; index++) {
        let day = dayjs(minDate).add(index, "day");
        day = this.formatDate(day);
        const contribution = this.dataJson[day] ?? 0;
        dates.push({ date: day, contribution });
      }
      return dates;
    },
    formatDate(date) {
      return dayjs(date).format("YYYY-MM-DD");
    },
    getSunday(minDate) {
      return this.formatDate(dayjs(minDate).day(0));
    },
  },
};
</script>

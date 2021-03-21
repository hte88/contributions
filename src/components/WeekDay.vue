<template>
  <ul class="days">
    <li v-for="(day, index) in dayWeek" :key="index" :title="day.long">
      {{ day.short }}
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    dayWeek: {
      Type: Array,
      default: () => [
        { short: "Su", long: "Sunday" },
        { short: "Mo", long: "Monday" },
        { short: "Tu", long: "Tuesday" },
        { short: "We", long: "Wenesday" },
        { short: "Th", long: "Thursday" },
        { short: "Fr", long: "Friday" },
        { short: "Sa", long: "Saturday" },
      ],
    },
  },
};
</script>

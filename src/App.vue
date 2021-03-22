<template>
  <div class="container mx-auto lg:w-3/4 xl:w-4/5">
    <div class="header">
      <h1 class="text-green-500 text-6xl font-bold text-center">
        Contributions
      </h1>
      <h4 class="text-green-500 text-xl font-semibold mt-10 mb-5">
        Objectifs:
      </h4>
      <ul class="text-gray-200 text-base">
        <li>Développer un composant uniquement en VueJS</li>
        <li>
          Au passage de la souris sur une case, on doit voir le nombre exacte de
          contributions
        </li>
        <li>
          L'échelle (en bas à gauche) doit être visible, elle est statique
        </li>
      </ul>
    </div>
    <ContributionTable :data-json="dataJSON"></ContributionTable>
    <ContributionTable :data-json="dataJSONBis" :color="style"></ContributionTable>
  </div>
</template>
<script>
import dataJSON from "./assets/data.json";
import dataJSONBis from "./assets/dataBis.json";
import ContributionTable from "./components/ContributionTable.vue";
export default {
  name: "App",
  data() {
    return {
      dataJSON: dataJSON,
      dataJSONBis: dataJSONBis,
      style: [
        { min: 0, max: 0, color: "#ebedf0" },
        { min: 1, max: 9, color: "#c6e48b" },
        { min: 10, max: 19, color: "#7bc96f" },
        { min: 20, max: 29, color: "#196127" },
        { min: 30, max: 1000, color: "#124f1d" },
      ],
    };
  },
  components: { ContributionTable },
};
</script>

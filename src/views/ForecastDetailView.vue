<template>
  <div id="forecast-detail">
    <InfoBar />
    <ForecastDetail />
  </div>
</template>

<script>
import InfoBar from "../components/InfoBar.vue";
import ForecastDetail from "../components/ForecastDetail.vue";

export default {
  components: {
    InfoBar,
    ForecastDetail,
  },
};
</script>

<style scoped></style>

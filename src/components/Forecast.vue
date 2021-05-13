<template>
  <div class="foreCast">
    <div class="tab">
      <button>Today</button>
      <button>Tomorrow</button>
      <span><a href="#">See All</a></span>
    </div>
    <div id="info">
      <div v-for="day of todayInfo" :key="day.index">
        <img :src="getIcon(day.time)" alt="" />
        <div>&#176;</div>
        <div>{{ getTime(day.time) }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todayInfo: Array,
    tomorrowInfo: Array,
  },

  computed: {
    getIcon(day) {
      let nameFile;
      let hour = day.toString().split(" ")[1];
      let hourInt = parseInt(hour.split(":")[0]);
      if (day.weather.toString().includes("rain") == true) {
        if (hourInt < 18) {
          nameFile = "rain";
        } else {
          nameFile = "rainnight";
        }
      } else if (day.weather.toString().includes("cloud") == true) {
        if (hourInt < 18) {
          nameFile = "cloudy";
        } else {
          nameFile = "cloudynight";
        }
      } else {
        if (hourInt < 18) {
          nameFile = "clear";
        } else {
          nameFile = "clearnight";
        }
      }
      return require(`../assets/${nameFile}.png`);
    },

    getTime(time) {
      let hour = time.toString().split(" ")[1];
      let hourInt = parseInt(hour.split(":")[0]);
      if (hourInt > 18) {
        return "Night";
      } else if (hourInt > 12) {
        return "Evening";
      } else if (hourInt > 9) {
        return "Afternoon";
      } else {
        return "Morning";
      }
    },
  },

  methods: {
    async logWeather() {
      console.log(this.todayInfo);
      console.log(this.tomorrowInfo);
    },
  },

  created() {
    this.logWeather();
  },
};
</script>

<style scoped>
.foreCast {
  padding-left: 5px;
  padding-right: 5px;
}

.tab {
  overflow: hidden;
  /* border: 1px solid #ccc; */
  background-color: #f1f1f1;
  margin-bottom: 20px;
}

/* Style the buttons that are used to open the tab content */
.tab button {
  background-color: #f1f1f1;
  float: left;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 14px 16px;
  transition: 0.3s;
}

.tab span {
  float: right;
  color: blue;
}

/* Change background color of buttons on hover */
.tab button:hover {
  background-color: #ddd;
}

/* Create an active/current tablink class */
.tab button.active {
  background-color: #ccc;
  font-weight: bold;
  font-size: 15px;
}

#info {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
</style>

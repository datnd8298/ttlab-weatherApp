<template>
  <div class="fore-cast">
    <div class="info-block">
      <div class="tab">
        <div class="tab-content">
          <div
            class="content-button"
            @click="todayForecast"
            :active="todayActive"
          >
            Today
          </div>
          <div
            class="content-button"
            @click="tomorrowForecast"
            :active="tomorrowActive"
          >
            Tomorrow
          </div>
        </div>
        <div class="detail-info">
          <router-link to="/forecast" :dayTime="dayTime"
            ><button>See All</button></router-link
          >
        </div>
      </div>
      <div class="info">
        <div v-for="(day, index) of forecastInfo" :key="index">
          <img :src="require(`../assets/${getIcon(day, index)}.png`)" alt="" />
          <div>{{ getTemp(day) }}&#176;</div>
          <div>{{ timeOfDay[index] }}</div>
        </div>
      </div>
    </div>
    <div class="info-block">
      <div class="tab">
        <div class="tab-content">
          <span>Air Polutions</span>
        </div>
        <div class="detail-info">
          <a href="#"><button>Details</button></a>
        </div>
      </div>
      <div id="air-polution-info">
        <div id="air-polution-img">
          <img src="../assets/unhealthy-icon.png" alt="" />
        </div>
        <div>
          <span
            >162 <span style="font-size: 13px">| Micro Dust / PM2.5</span></span
          >
          <br />
          <span style="font-size: 13px">Unhealthy</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      timeOfDay: ["Morning", "Afternoon", "Evening", "Night"],
      forecastInfo: {},
      todayActive: "0",
      tomorrowActive: "0",
      dayTime: "Today",
    };
  },
  props: {
    todayInfo: Array,
    tomorrowInfo: Array,
  },

  methods: {
    getTemp(day) {
      return Math.floor(day.main.temp - 273.15);
    },

    getIcon(day, index) {
      let nameFile;
      if (index < 2) {
        if (day.weather[0].description.includes("rain") == true) {
          nameFile = "rain";
        } else if (day.weather[0].description.includes("cloud") == true) {
          nameFile = "cloudy";
        } else if (day.weather[0].description.includes("cloud") == true) {
          nameFile = "clear";
        } else {
          nameFile = "nice";
        }
      } else {
        if (day.weather[0].description.includes("rain") == true) {
          nameFile = "rain";
        } else if (day.weather[0].description.includes("cloud") == true) {
          nameFile = "cloudy";
        } else if (day.weather[0].description.includes("cloud") == true) {
          nameFile = "clear";
        } else {
          nameFile = "nice";
        }
      }
      return nameFile;
    },

    todayForecast() {
      this.forecastInfo = this.todayInfo;
      this.todayActive = "1";
      this.tomorrowActive = "0";
      this.dayTime = "Today";
      // console.log(this.todayInfo);
    },

    tomorrowForecast() {
      this.forecastInfo = this.tomorrowInfo;
      this.todayActive = "0";
      this.tomorrowActive = "1";
      this.dayTime = "Tomorrow";
    },
  },

  created() {
    this.todayForecast();
  },
};
</script>

<style scoped>
.fore-cast {
  padding-left: 5px;
  padding-right: 5px;
}

.info-block {
  margin-top: 20px;
}

.tab {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  overflow: hidden;
  margin-bottom: 20px;
}

/* Style the buttons that are used to open the tab content */
.content-button {
  background-color: white;
  border: none;
  outline: none;
  cursor: pointer;
  margin-right: 20px;
  transition: 0.3s;
}

/* Change background color of buttons on hover */
.content-button:hover {
  font-weight: bold;
}

/* Create an active/current tablink class */
.content-button[active="1"] {
  font-weight: bold;
}

.detail-info {
  display: flex;
  align-items: center;
}

.detail-info button {
  background-color: white;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 14px 16px;
  transition: 0.3s;
  color: blue;
}

.info {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.info div {
  text-justify: center;
}

.tab-content {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.tab-content span {
  font-weight: bold;
}

#air-polution-info {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  font-size: 40px;
  font-weight: bold;
}

#air-polution-img {
  display: flex;
  align-content: center;
  width: 90px;
}

#air-polution-img img {
  max-height: 80px;
  max-width: 90px;
}
</style>

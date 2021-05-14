<template>
  <div id="forecast-detail">
    <div class="function-tab">
      <router-link to="/"
        ><img src="../assets/backArrow.png" alt=""
      /></router-link>
      <div id="time-info">
        <span>{{ dayTime }} Today</span>
      </div>
    </div>
    <div class="info-block">
      <div class="block-title">
        <span>{{ dateTime }}</span>
      </div>
      <div
        class="detail-block"
        v-for="(info, index) of forecastInfo"
        :key="index"
      >
        <div><img src="../assets/Ellipse 25.png" alt="" /></div>
        <div>
          <img :src="require(`../assets/${getIcon(info, index)}.png`)" alt="" />
          <br />
          <span>{{ timeOfDay[index] }}</span>
        </div>
        <div id="weather-des">
          <span style="font-weight: bold">{{ getTemp(info) }}&#176;</span>
          <br />
          <span>{{ getWeatherDes(info) }}</span>
        </div>
      </div>
    </div>
    <div class="details-block">
      <div class="block-title">
        <span>Today Details</span>
      </div>
      <div id="detail-list">
        <div
          class="day-detail-block"
          v-for="(info, index) of forecastInfo"
          :key="index"
        >
          <div>
            <img
              :src="require(`../assets/${getDetailIcon(index)}Icon.png`)"
              alt=""
            />
          </div>
          <div id="detail-info">
            <span style="font-weight: bold">{{ getDetail(info, index) }}</span>
            <br />
            <span>{{ dayDetails[index] }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      timeOfDay: ["Morning", "Afternoon", "Evening", "Night"],
      dayDetails: ["Wind", "Humidity", "UV Index", "Pressure"],
      backgroundColor: ["blue", "yellow", "red", "green"],
      forecastInfo: [],
      dateTime: String,
    };
  },

  props: {
    dayTime: String,
  },

  methods: {
    async getWeatherInfo() {
      await axios(
        "http://api.openweathermap.org/data/2.5/forecast?q=Hanoi,vn&mode=json&appid=c884e79cb699c1a98e4e8d01547ba93e"
      )
        .then((response) => {
          this.dateTime = new Date(response.data.list[0].dt * 1000).toLocaleDateString("en-US", { month: "long", day: "numeric" });
          this.forecastInfo.push(response.data.list[1]);
          this.forecastInfo.push(response.data.list[2]);
          this.forecastInfo.push(response.data.list[4]);
          this.forecastInfo.push(response.data.list[5]);
        })
        .catch((err) => {
          console.log(err);
        });
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

    getTemp(day) {
      return Math.floor(day.main.temp - 273.15);
    },

    getWeatherDes(day) {
      return day.weather[0].description;
    },

    getDetailIcon(index) {
      return this.dayDetails[index];
    },

    getDetail(day, index) {
      if (this.dayDetails[index].includes("Wind") == true) {
        return "E " + day.wind.speed + " kmh";
      } else if (this.dayDetails[index].includes("Humidity") == true) {
        return day.main.humidity + "%";
      } else if (this.dayDetails[index].includes("Pressure") == true) {
        return day.main.pressure + " hPa";
      } else {
        return "8";
      }
    },

    getColor(index) {
      return this.backgroundColor[index];
    },
  },

  created() {
    this.getWeatherInfo();
    console.log(this.dateTime);
  },
};
</script>

<style scoped>
.function-tab {
  display: flex;
  flex-direction: row;
  margin-top: 20px;
  font-size: 30px;
  font-weight: bold;
}

#time-info {
  margin-left: 160px;
}

.block-title {
  font-size: 30px;
  font-weight: bold;
}

.info-block {
  display: flex;
  flex-direction: column;
  align-content: space-between;
  margin-top: 30px;
}

.detail-block {
  margin-top: 20px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

#weather-des {
  font-size: 23px;
  width: 60%;
  background-color: skyblue;
}

.details-block {
  margin-top: 30px;
}

#detail-list {
  margin-top: 20px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  flex-wrap: wrap;
}

.day-detail-block {
  margin-top: 15px;
  display: flex;
  flex-direction: row;
  width: 50%;
  align-items: center;
}

#detail-info {
  margin-left: 10px;
  font-size: 25px;
}

.day-detail-block img {
  max-width: 100px;
  max-height: 100px;
}
</style>

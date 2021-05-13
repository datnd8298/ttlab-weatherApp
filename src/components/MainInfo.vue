<template>
  <div class="mainInfo">
    <div id="mainTemp">
      <div id="temp">
        <h1>
          {{ getTemp }} &#8451;
          <span style="font-size: 13px; font-weight: lighter">
            |{{ getWeather }}
          </span>
        </h1>
      </div>
      <div id="iconWeather">
        <img :src="getIcon" alt="" />
      </div>
    </div>
    <div id="moreInfo">
      <div id="location">
        <p style="font-weight: bold; font-size: 25px">{{ getCity }}</p>
        <p style="font-size: 15px">
          {{ getCountry }}
          <span><img src="../assets/selectionArrow.png" alt="" /></span>
        </p>
      </div>
      <div id="weatherInfo">
        <div>
          <span>{{ getHumidity }} %</span>
          <p>Humidity</p>
        </div>
        <div>
          <span>10</span>
          <p>UV Index</p>
        </div>
        <div>
          <span>{{ getWind }} KM/H</span>
          <p>Wind</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    getTemp() {
      return this.mainInfo.temp ? this.mainInfo.temp : "no info";
    },

    getHumidity() {
      return this.mainInfo.humidity ? this.mainInfo.humidity : "no info";
    },

    getWind() {
      return this.mainInfo.wind ? this.mainInfo.wind : "no info";
    },

    getWeather() {
      return this.mainInfo.weather ? this.mainInfo.weather : "no info";
    },

    getCity() {
      return this.mainInfo.city ? this.mainInfo.city : "no info";
    },

    getCountry() {
      return this.mainInfo.country ? this.mainInfo.country : "no info";
    },

    getIcon() {
      var nameFile = "nice";
      if (this.mainInfo.weather.toString().includes("rain") == true) {
        nameFile = "rain";
      } else if (this.mainInfo.weather.toString().includes("cloud") == true) {
        nameFile = "cloud";
      } else if (this.mainInfo.weather.toString().includes("sunny") == true) {
        nameFile = "sunny";
      } else if (this.mainInfo.weather.toString().includes("clear") == true) {
        nameFile = "clear";
      }
      return require(`../assets/${nameFile}.png`);
    },
  },

  props: {
    mainInfo: {},
  },
};
</script>

<style scoped>
.mainInfo {
  padding-left: 5px;
  padding-right: 5px;
}

#mainTemp {
  margin-top: 30px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

#temp {
  width: 60%;
  font-size: 25px;
}

#iconWeather {
  max-height: 200px;
}

#iconWeather img {
  height: 100px;
  width: 100px;
}

#moreInfo {
  text-align: left;
}

#location {
  margin-bottom: 30px;
}

#weatherInfo div {
  display: inline-block;
  text-align: center;
  width: 33%;
}

#weatherInfo span {
  font-weight: bold;
  text-align: center;
}
</style>

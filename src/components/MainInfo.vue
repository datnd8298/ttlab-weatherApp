<template>
  <div>
    <div id="mainTemp">
      <div id="temp">
        <h1>
          {{ getTemp }} &#8451;
          <span style="font-size: 15px; font-weight: lighter"
            >| {{ getWeather }}</span
          >
        </h1>
      </div>
      <div id="iconWeather">
        <img :src="getIcon" alt="" />
      </div>
      <div id="moreInfo">
        <div id="location">
          <p style="font-weight: bold; font-size: 25px">{{ getCity }}</p>
          <p style="font-size: 15px">{{ getCountry }}</p>
        </div>
        <div id="weatherInfo">
          <div>
            <span style="text-align: center">{{ getHumidity }} %</span>
            <p>Humidity</p>
          </div>
          <div>
            <span style="text-align: center">{{ getWind }} KM/H</span>
            <p>Wind</p>
          </div>
          <div>
            <span style="text-align: center">10</span>
            <p>UV Index</p>
          </div>
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
      if (this.mainInfo.weather.includes("rain") == true) {
        return "../assets/rain.png"
      } else if (this.mainInfo.weather.includes("cloud") == true) {
        return "../assets/cloudy.png"
      } else if (this.mainInfo.weather.includes("sunny") == true) {
        return "../assets/sunny.png"
      } else if (this.mainInfo.weather.includes("clear") == true) {
        return "../assets/clear.png"
      }
      return "../assets/nice.png"
    }
  },

  props: {
    mainInfo: {},
  },
};
</script>

<style scoped>
#temp {
  width: 50%;
  display: inline-block;
  font-size: 25px;
}

#iconWeather {
  max-height: 200px;
  width: 50%;
  display: inline-block;
}

#iconWeather img {
  height: 100px;
  width: 150px;
}

#moreInfo {
  text-align: left;
  padding-left: 200px;
}

#location {
  padding-bottom: 50px;
}

#weatherInfo div {
  display: inline-block;
  width: 30%;
}

#weatherInfo div span {
  font-weight: bold;
}
</style>

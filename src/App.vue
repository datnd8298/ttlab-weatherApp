<template>
  <div id="app">
    <MainInfo :mainInfo="mainInfo" />
    <Forecast :today="todayInfo" :tomorrow="tomorrowInfo" />
  </div>
</template>

<script>
import MainInfo from "./components/MainInfo.vue";
import Forecast from "./components/Forecast.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    MainInfo,
    Forecast,
  },

  data() {
    return {
      weatherInfo: {},

      dayWeather: {
        time: "",
        temp: Number,
        weather: String
      },

      mainInfo: {
        temp: Number,
        humidity: Number,
        wind: Number,
        weather: String,
        city: String,
        country: "Viet Nam"
      },

      todayInfo: [],

      tomorrowInfo: []
    }
  },

  methods: {
    async getWeatherInfo() {
      await axios("http://api.openweathermap.org/data/2.5/forecast?q=Hanoi,vn&mode=json&appid=c884e79cb699c1a98e4e8d01547ba93e")
        .then((response) => {
          this.weatherInfo = response.data

          for (let i = 1; i < 7; i++) {
            this.dayWeather.temp = Math.floor(this.weatherInfo.list[i].main.temp - 273.15)
            this.dayWeather.weather = this.weatherInfo.list[i].weather[0].description
            this.todayInfo.push(this.dayWeather)
          }

          for (let i = 9; i < 15; i++) {
            this.dayWeather.temp = Math.floor(this.weatherInfo.list[i].main.temp - 273.15)
            this.dayWeather.weather = this.weatherInfo.list[i].weather[0].description
            this.tomorrowInfo.push(this.dayWeather)
          }
          var sum = 0;
          this.mainInfo.temp = Math.floor(this.todayInfo.forEach((a) => {
            return sum+=a
          }) / this.todayInfo.length)
          this.mainInfo.humidity = this.weatherInfo.list[0].main.humidity
          this.mainInfo.wind = this.weatherInfo.list[0].wind.speed
          this.mainInfo.weather = this.weatherInfo.list[0].weather[0].description
          this.mainInfo.city = this.weatherInfo.city.name
        })
        .catch((error) => {
          console.log(error.response);
        })
    }
  },

  created() {
    this.getWeatherInfo()
    console.log(this.mainInfo);
    console.log(this.todayInfo);
    console.log(this.tomorrowInfo);
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

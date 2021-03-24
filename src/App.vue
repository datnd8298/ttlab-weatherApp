<template>
  <div id="app">
    <MainInfo :mainInfo="mainInfo" />
    <Forecast :today="todayInfo" :tomorrow="tomorrowInfo"/>
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

      mainInfo: {
        temp: Number,
        humidity: Number,
        wind: Number,
        weather: String,
        city: String,
        country: "Viet Nam"
      },
      
      todayInfo: {
        morning: Number,
        afternoon: Number,
        evening: Number,
        night: Number,
        morningWeather: String,
        afternoonWeather: String,
        eveningWeather: String,
        nightWeather: String
      },

      tomorrowInfo: {
        morning: Number,
        afternoon: Number,
        evening: Number,
        night: Number,
        morningWeather: String,
        afternoonWeather: String,
        eveningWeather: String,
        nightWeather: String
      }
    }
  },

  methods: {
    async getWeatherInfo() {
      await axios("http://api.openweathermap.org/data/2.5/forecast?q=Hanoi,vn&mode=json&appid=c884e79cb699c1a98e4e8d01547ba93e")
        .then((response) => {
          this.weatherInfo = response.data

          this.todayInfo.morning = Math.floor(this.weatherInfo.list[1].main.temp - 273.15)
          this.todayInfo.afternoon = Math.floor(this.weatherInfo.list[3].main.temp - 273.15)
          this.todayInfo.evening = Math.floor(this.weatherInfo.list[5].main.temp - 273.15)
          this.todayInfo.night = Math.floor(this.weatherInfo.list[6].main.temp - 273.15)
          this.todayInfo.morningWeather = this.weatherInfo.list[1].weather[0].description
          this.todayInfo.afternoonWeather = this.weatherInfo.list[3].weather[0].description
          this.todayInfo.eveningWeather = this.weatherInfo.list[5].weather[0].description
          this.todayInfo.nightWeather = this.weatherInfo.list[6].weather[0].description

          this.tomorrowInfo.morning = Math.floor(this.weatherInfo.list[9].main.temp - 273.15)
          this.tomorrowInfo.afternoon = Math.floor(this.weatherInfo.list[11].main.temp - 273.15)
          this.tomorrowInfo.evening = Math.floor(this.weatherInfo.list[13].main.temp - 273.15)
          this.tomorrowInfo.night = Math.floor(this.weatherInfo.list[14].main.temp - 273.15)
          this.tomorrowInfo.morningWeather = this.weatherInfo.list[9].weather[0].description
          this.tomorrowInfo.afternoonWeather = this.weatherInfo.list[11].weather[0].description
          this.tomorrowInfo.eveningWeather = this.weatherInfo.list[13].weather[0].description
          this.tomorrowInfo.nightWeather = this.weatherInfo.list[14].weather[0].description
          
          this.mainInfo.temp = Math.floor((this.todayInfo.morning + this.todayInfo.afternoon + this.todayInfo.evening + this.todayInfo.night)/4)
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

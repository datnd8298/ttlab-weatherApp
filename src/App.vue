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
        weather: String,
      },

      mainInfo: {
        temp: Number,
        humidity: Number,
        wind: Number,
        weather: String,
        city: String,
        country: "Viet Nam",
      },

      todayInfo: [],

      tomorrowInfo: [],

      forecastToday: [],

      forecastTomorrow: []
    };
  },

  methods: {
    async getWeatherInfo() {
      await axios(
        "http://api.openweathermap.org/data/2.5/forecast?q=Hanoi,vn&mode=json&appid=c884e79cb699c1a98e4e8d01547ba93e"
      )
        .then((response) => {
          this.weatherInfo = response.data;

          this.forecastToday.push(this.weatherInfo.list[1])
          this.forecastToday.push(this.weatherInfo.list[3])
          this.forecastToday.push(this.weatherInfo.list[5])
          this.forecastToday.push(this.weatherInfo.list[6])

          this.forecastTomorrow.push(this.weatherInfo.list[9])
          this.forecastTomorrow.push(this.weatherInfo.list[11])
          this.forecastTomorrow.push(this.weatherInfo.list[13])
          this.forecastTomorrow.push(this.weatherInfo.list[14])

          for (let i = 0; i < 4; i++) {
            this.dayWeather.temp = Math.floor(
              this.forecastToday[i].main.temp - 273.15
            );
            this.dayWeather.weather = this.forecastToday[i].weather[0].description;
            this.dayWeather.time = this.forecastToday[i].dt_txt;
            this.todayInfo.push(this.dayWeather);
          }

          for (let j = 0; j < 4; j++) {
            this.dayWeather.temp = Math.floor(
              this.forecastTomorrow[j].main.temp - 273.15
            );
            this.dayWeather.weather = this.forecastTomorrow[j].weather[0].description;
            this.dayWeather.time = this.forecastToday[j].dt_txt;
            this.tomorrowInfo.push(this.dayWeather);
          }
          var sum = 0;
          this.todayInfo.forEach((element) => {
            sum = sum + element.temp;
          });
          this.mainInfo.temp = Math.floor(sum / this.todayInfo.length);
          this.mainInfo.humidity = this.weatherInfo.list[0].main.humidity;
          this.mainInfo.wind = this.weatherInfo.list[0].wind.speed;
          this.mainInfo.weather = this.weatherInfo.list[0].weather[0].description;
          this.mainInfo.city = this.weatherInfo.city.name;
        })
        .catch((error) => {
          console.log(error.response);
        });
    },
  },

  created() {
    this.getWeatherInfo();
  },
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

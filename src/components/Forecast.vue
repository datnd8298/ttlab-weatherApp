<template>
  <div id="container">
    <div class="tab">
      <button class="tablinks">Today</button>
      <button class="tablinks">Tomorrow</button>
      <span><a href="#">See All</a></span>
    </div>
    <div id="info">
      <div v-for="(day, index) of today" :key="index">
        <div><img :src="getIcon(day.time)" alt=""></div>
        <div>{{getTime(day.time)}} &#176;</div>
        <div></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    today: [Object],
    tomorrow: [Object],
  },

  computed: {
    getIcon(day) {
      let hour = day.split(" ")[1]
      let hourInt = parseInt(hour.split(":")[0])
      if(day.weather.includes("rain") == true){
        if(hourInt < 18){
          return "../assets/rain.png"
        } else{
          return "../assets/rainnight.png"
        }
      } else if(day.weather.includes("cloud") == true){
        if(hourInt < 18){
          return "../assets/cloudy.png"
        } else{
          return "../assets/cloudynight.png"
        }
      } else {
        if(hourInt < 18){
          return "../assets/clear.png"
        } else{
          return "../assets/clearnight.png"
        }
      }
    },

    getTime(time){
      let hour = time.split(" ")[1]
      let hourInt = parseInt(hour.split(":")[0])
      if(hourInt > 18) {
        return "Night"
      } else if (hourInt > 12){
        return "Evening"
      } else if (hourInt > 9) {
        return "Afternoon"
      } else {
        return "Morning"
      }
    }
  }
};
</script>

<style scoped>
#container {
  padding-left: 200px;
  padding-right: 380px;
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

#info div {
  display: inline-block;
  width: 25%;
}
</style>

<template>
  <div>
    <div id="mobileInfo">
      <div id="clock">
        <span>{{ getTime }}</span>
      </div>
      <div id="generalInfo">
        <span><img src="../assets/Cellular Connection.png" alt="" /></span>
        <span><img src="../assets/Wifi.png" alt="" /></span>
        <span><img src="../assets/Battery.png" alt="" /></span>
      </div>
    </div>
    <div id="register">
      <div id="noticeIcon">
        <a href="#">
          <img src="../assets/noticeIcon.png" alt="" />
        </a>
      </div>
      <div id="avatar">
        <a href="#">
          <img src="../assets/avatar.png" alt="" />
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    getTime() {
      var time = new Date();
      return time.getHours() + ":" + time.getMinutes();
    },
  },
};
</script>

<style scoped>
#clock span {
  font-weight: bold;
}

#mobileInfo {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

#generalInfo span {
  margin-left: 5px;
  margin-right: 5px;
}

#clock span {
  margin-left: 20px;
}

#register {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
}

#noticeIcon {
  margin-right: 20px;
  padding-top: 5px;
}

#avatar {
  margin-right: 5px;
}
</style>

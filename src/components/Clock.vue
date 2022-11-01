<template>
  <div class="container">
    <div class="clock" :style="clockStyle">
      <div class="clock-outer-border">
        <div class="clock-inner-border">
          <div class="clock-hour" v-for="(hour, index) in hours" :key="index">
            {{ hour }}
          </div>

          <div class="point">
            <div class="point-hour" :style="hourStyle"></div>
            <div class="point-minute" :style="minuteStyle"></div>
            <div class="point-second" :style="secondStyle"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CLock",
  data() {
    return {
      hours: ["Ⅰ", "Ⅱ", "Ⅲ", "Ⅳ", "Ⅴ", "Ⅵ", "Ⅶ", "Ⅷ", "Ⅸ", "Ⅹ", "Ⅺ", "Ⅻ"],
      date: new Date(),
    };
  },
  computed: {
    hourStyle() {
      let value = this.date.getHours();
      return {
        transform: `translateY(-50%) rotate(${value * 30 - 90}deg)`,
      };
    },
    minuteStyle() {
      let value = this.date.getMinutes();
      return {
        transform: `translateY(-50%) rotate(${value * 6 - 90}deg)`,
      };
    },
    secondStyle() {
      let value = this.date.getSeconds();
      return {
        transform: `translateY(-50%) rotate(${value * 6 - 90}deg)`,
      };
    },
    clockStyle() {
      let value = this.date.getSeconds();
      // rgba(255, 255, 255, 0.466)
      let color = "";
      for (let i = 0; i < 60; i++) {
        if (i != 0) {
          color += ",";
        }
        if (i == value) {
          color += " rgba(255, 255, 255, 0.466)";
        } else {
          color += "transparent";
        }
      }
      console.log(value);
      return {
        "background-image": `conic-gradient(${color})`,
      };
    },
  },
  methods: {
    init() {
      this.setTime();
      setInterval(() => {
        this.setTime();
      }, 1000);
    },
    setTime() {
      this.date = new Date();
      //   let _hour = date.getHours();
      //   let _munites = date.getMinutes();
      //   let _second = date.getSeconds();
      //   console.log("_hour", _hour);
      //   console.log("_munites", _munites);
      //   console.log("_second", _second);
    },
  },
  mounted() {
    this.init();
  },
};
</script>

<style>
.container {
  height: 100vh;
  width: 100vw;
  background: #011121;
}

.clock {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 999px;
  background-color: #011121;
}
.clock-outer-border {
  width: 500px;
  height: 500px;
  border: 5px solid rgb(31, 128, 217);
  border-radius: 999px;
  padding: 5px;
  box-shadow: 0px 0px 16px 9px #1d399d;
}
.clock-inner-border {
  width: 480px;
  height: 480px;
  border: 5px dashed rgb(78, 154, 224);
  border-radius: 999px;
  box-shadow: 0px 0px 16px 9px #1d399d;
}

.clock-hour {
  font-size: 40px;
  color: rgb(90, 159, 222);
  position: absolute;
  /* text-shadow: 0px 0px 16px 9px rgb(90, 159, 222); */
  text-shadow: 0 0 10px #0e45ab, 0 0 20px #376ac9, 0 0 30px #3e59bf,
    0 0 40px #0b158b;
}
.clock-hour:nth-of-type(1) {
  top: 9%;
  right: 26%;
}
.clock-hour:nth-of-type(2) {
  top: 25%;
  right: 11%;
}
.clock-hour:nth-of-type(3) {
  top: 45%;
  right: 5%;
}
.clock-hour:nth-of-type(4) {
  top: 66%;
  right: 11%;
}
.clock-hour:nth-of-type(5) {
  top: 80%;
  right: 26%;
}
.clock-hour:nth-of-type(6) {
  top: 86%;
  right: 46%;
}
.clock-hour:nth-of-type(7) {
  top: 80%;
  right: 66%;
}
.clock-hour:nth-of-type(8) {
  top: 66%;
  right: 80%;
}
.clock-hour:nth-of-type(9) {
  top: 45%;
  right: 85%;
}
.clock-hour:nth-of-type(10) {
  top: 25%;
  right: 80%;
}
.clock-hour:nth-of-type(11) {
  top: 9%;
  right: 66%;
}
.clock-hour:nth-of-type(12) {
  top: 5%;
  right: 46%;
}

.point {
  position: absolute;
  top: 50%;
  left: 50%;
  background: rgb(38, 100, 233);
  border-radius: 999px;
}

.point-hour {
  position: absolute;
  width: 80px;
  /* border-top: 5px solid rgb(9, 239, 236); */
  /* border-bottom: 5px solid rgb(3, 30, 234); */
  height: 10px;
  background: rgb(182, 168, 168);
  transform-origin: left center;
  box-shadow: 0px 0px 20px 4px #1512b7;
}

.point-minute {
  position: absolute;
  height: 6px;
  width: 140px;
  background: rgb(129, 121, 121);
  transform-origin: left center;
  box-shadow: 0px 0px 20px 3px #1d399d;
}

.point-second {
  position: absolute;
  height: 5px;
  width: 150px;
  background: rgb(90, 85, 85);
  transform-origin: left center;
  box-shadow: 0px 0px 50px 9px #1d399d;
}

.box {
  border-radius: 16px;
  border: 10px solid;
  border-image: linear-gradient(#8f41e9, #578aef, #ff5277) 30 30;
  animation: light 3s linear infinite;
}

@keyframes light {
  0% {
    filter: hue-rotate(0deg); /*色调旋转*/
  }

  20% {
    filter: hue-rotate(100deg); /*色调旋转*/
  }

  40% {
    filter: hue-rotate(200deg); /*色调旋转*/
  }

  100% {
    filter: hue-rotate(360deg); /*色调旋转*/
  }
}
</style>

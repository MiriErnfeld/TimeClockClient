
<template>
  <div class="container">
    <h3>Time Clock</h3>
    <div class="clock-border">
      <div class="clock-inner" :class="color">
        <div class="hour">{{ hours }}</div>
        <div class="dots">:</div>
        <div class="min">{{ minutes }}</div>
        <div class="dots">:</div>
        <div class="secs">{{ seconds }}</div>
        <div class="mode"></div>
      </div>
      <div>
        <div class="details">
          name : <input type="text" v-model="name" /> id:<input
            type="text"
            v-model="userId"
          />
        </div>
        <div class="divbtn">
          <button v-on:click="createShift" class="btn">Entrance</button>
          <button v-on:click="endShift" class="btn">Exit</button>
        </div>
      </div>
    </div>
    <!-- <router-link to="/Users">shift manage</router-link> -->
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "DigitalClock",
  data() {
    return {
      hours: 0,
      minutes: 0,
      seconds: 0,
      time: null,
      time1: null,
      time2: null,
      end1: null,
      end2: null,
      users: null,
      name: "",
      userId: "",
      shiftId: "",
    };
  },
  methods: {
    // allShifts: function () {
    //   this.$router.push("Users");
    // },
    createShift: function () {
      this.time1 = this.time.slice(0, 2);
      this.time2 = this.time1 + ":" + this.minutes + ":" + this.seconds;
      const options = { name: this.name, enterTime: this.time2 };
      axios
        .post(`http://localhost:3007/createShift/${this.userId}`, options)
        .then((res) => {
          console.log(res);
          alert("you start your shift!");
        });
    },
    endShift: function () {
      this.end1 = this.time.slice(0, 2);
      this.end2 = this.end1 + ":" + this.minutes + ":" + this.seconds;
      const options = { leavingTime: this.end2 };
      console.log(options);
      axios
        .post(`http://localhost:3007/updateShift/${this.userId}`, options)
        .then((res) => {
          alert("you finished your shift!");
          console.log("end" + res.data);
        });
    },
    setTime() {
      setInterval(() => {
        const date = new Date();
        this.hours = date.getHours();
        this.minutes = this.checkSingleDigit(date.getMinutes());
        this.seconds = this.checkSingleDigit(date.getSeconds());
      }, 1000);
    },
    checkSingleDigit(digit) {
      this.time = this.hours + this.minutes + this.seconds;
      return ("0" + digit).slice(-2);
    },
  },
  mounted() {
    this.setTime();
  },
};
</script>
<style>
.divbtn {
  display: flex;
  justify-content: space-around;
}

.details {
  margin-bottom: 3%;
}
.btn:hover {
  color: white;
}
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: auto;
  flex-direction: column;
}
.hour,
.min,
.secs {
  font-size: 7em;
}
strong {
  color: blue;
}

.clock-border {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 700px;
  height: 300px;
  background: whitesmoke;
  flex-wrap: wrap;
}
.clock-inner {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 600px;
  height: 150px;
  background: white;
  border-radius: 20px;
  color: black;
}

.btn {
  font-size: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 105px;
  height: 50px;
  background: black;
  border-radius: 20px;
  color: white;
}
.dots {
  font-size: 70px;
}
</style>


   
<template>
  <div>
    <div>
      enter name : <input type="text" v-model="name" /> enter id:<input
        type="text"
        v-model="userId"
      />
    </div>
    <div class="div-btn">
      <button v-on:click="createShift" class="btn">Entrance</button>
      <button v-on:click="endShift" class="btn">Exit</button>
      <!-- <button v-on:click="AllShifts">All Shifts</button> -->
    </div>
  </div>
</template>

<script>
import axios from "axios";
// import Users from "./Users.vue";

export default {
  name: "EnterExit",
  props: {
    color: {
      type: String,
      default: "red",
    },
  },
  data() {
    return {
      users: null,
      name: "",
      userId: "",
      date: new Date(),
    };
  },
  methods: {
    createShift: function () {
      alert(this.date);
      const options = { name: this.name };
      // axios.post('https://reqres.in/api/articles', article)
      axios
        .post(`http://localhost:3007/createShift/${this.userId}`, options)
        .then((res) => {
          console.log(res);
          this.users = res.data;
          alert("enter new user");
          alert("name: " + this.name + "id: " + this.id + " data: ");
        });
    },
    endShift: function () {
      axios.get("http://localhost:3007/getAllShifts").then((res) => {
        this.users = res.data;
        alert("end" + res.data);
      });
    },
    // AllShifts: function () {
    //   alert("users");
    //   this.$router.push("/Users");
    // },
  },
};
</script>

<style>
.div-btn {
  display: flex;
  align-items: center;
  width: 300px;
  height: 100px;
  background: linear-gradient(to right, grey, rgb(82, 76, 76));
  margin-top: 4%;
  justify-content: space-around;
  margin-left: 38%;
}

.btn:hover {
  color: white;
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
  color: red;
}
</style>

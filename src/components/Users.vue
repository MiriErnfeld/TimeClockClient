<template>
  <div>
    <div class="div-table">
      <spam class="spam"> All Users:</spam>
      <table class="pure-table">
        <thead>
          <tr>
            <th scope="col">name</th>
            <th scope="col">User Id</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in allUsers" v-bind:key="user._id">
            <td>{{ user.name }}</td>
            <td>{{ user.userId }}</td>
          </tr>
        </tbody>
      </table>
      <spam class="spam"> All Shifts:</spam>
      <table class="pure-table">
        <thead>
          <tr>
            <th scope="col">Name</th>
            <th scope="col">start</th>
            <th scope="col">end</th>
            <th scope="col">-</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="shift in shifts" v-bind:key="shift._id">
            <td>{{ shift.userId.name }}</td>
            <td>{{ shift.enterTime }}</td>
            <td>{{ shift.leavingTime }}</td>
            <td>
              <button
                value="key"
                type="button"
                v-on:click="deleteShift(shift, shift._id, shift.userId._id)"
              >
                delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Users",
  data() {
    return {
      allUsers: null,
      shifts: null,
      shifts2: null,
      userId: "",
      i: "",
    };
  },
  created: function () {
    axios.get("http://localhost:3007/getAllUsers").then((res) => {
      this.allUsers = res.data;
    });
    axios.get("http://localhost:3007/getAllShifts").then((res) => {
      this.shifts = res.data;
    });
  },
  methods: {
    deleteShift: function (all, shiftId, userId) {
      console.log(this.shifts);
      alert("are you shure that you wont deleted?");
      const options = { userId: userId };
      axios
        .post(`http://localhost:3007/deleteShift/${shiftId}`, options)
        .then((res) => {
          console.log(res);
          // this.shifts.$remove(all); //this code not working?
        })
        .bind(this);
    },
  },
};
</script>
<style>
.spam {
  margin-right: 2%;
  margin-left: 2%;
  font-weight: bold;
}
.div-table {
  margin-top: 8%;
  display: flex;
  justify-content: center;
}
h3 {
  margin-bottom: 5%;
}
</style>
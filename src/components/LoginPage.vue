<template>
  <img class="logo" src="../assets/logo-R.png" alt="" />
  <h1>Login</h1>
  <div class="login">
    <!-- <input type="text" placeholder="Enter name" v-model="name" /> -->
    <input type="text" placeholder="Enter email" v-model="email" />
    <input type="password" placeholder="Enter password" v-model="password" />
    <button v-on:click="login">Login</button>
    <p>
      <router-link to="/signup">SingUp</router-link>
    </p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "LoginPage",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      let results = await axios.get(
        `http://localhost:3000/users?email=${this.email}&${this.password}`
      );
      console.log(results);
      if (results.status == 200 && results.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(results.data));
        this.$router.push({ name: "HomePage" });
      }
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "HomePage" });
    }
  },
};
</script>


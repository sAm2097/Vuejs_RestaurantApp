<template>
  <div class="nav">
    <router-link to="/">Home</router-link>
    <router-link to="/add">Add Restaurant</router-link>

    <a v-on:click="logout" href="#">Logout</a>
  </div>
</template>
<script>
export default {
  name: "TheHeader",
  methods: {
    logout() {
      localStorage.clear();
      this.$router.push({ name: "LoginPage" });
    },
  },
};
</script>

<style scoped>
.nav {
  background-color: rgb(63, 131, 241);
  overflow: hidden;
}
.nav a {
  float: left;
  color: aliceblue;
  padding: 16px 14px;
  text-align: center;
  text-decoration: none;
  margin-right: 5px;
  font-size: 17px;
}
.nav a:hover {
  background: darkgoldenrod;
  color: azure;
}
</style>
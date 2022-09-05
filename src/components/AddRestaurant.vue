<template>
  <the-header> </the-header>
  <h1>Hey {{name}}, Add Restaurant</h1>
  <form action="" class="add">
    <input
      type="text"
      name="name"
      placeholder="Enter name"
      v-model="restaurant.name"
    />
    <input
      type="text"
      name="address"
      placeholder="Enter address"
      v-model="restaurant.address"
    />
    <input
      type="text"
      name="contact"
      placeholder="Enter contact"
      v-model="restaurant.contact"
    />
    <button type="button" v-on:click="addRestaurant">Add new restaurant</button>
  </form>
</template>
<script>
import TheHeader from "./TheHeader.vue";
import axios from 'axios'
export default {
  name: "AddRestaurant",
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  methods: {
    async addRestaurant() {
      const result=await axios.post("http://localhost:3000/restaurant",
      {
      name:this.restaurant.name,
      address:this.restaurant.address,
      contact:this.restaurant.contact
      })
      if(result.status==201)
      {
        this.$router.push({name:'HomePage'})
      }
      console.log(result)
    },
  },
  components: {
    TheHeader,
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>
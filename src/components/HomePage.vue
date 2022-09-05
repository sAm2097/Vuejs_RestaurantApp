<template>
  <the-header> </the-header>
  <h1>Hello {{ name }}, welcome to HomePage</h1>
  <table border="1px">
    <tr>
      <td>Id</td>
      <td>Name</td>
      <td>Contact</td>
      <td>Address</td>
      <td>Actions</td>
    </tr>
    <tr v-for="item in restaurant" :key="item.id">
      <td>
        {{ item.id }}
      </td>
      <td>
        {{ item.name }}
      </td>
      <td>
        {{ item.contact }}
      </td>
      <td>
        {{ item.address }}
      </td>
      <td>
       <router-link :to="'/update/'+item.id">Update</router-link>
       <br>
       <button v-on:click="deleteRes(item.id)">Delete</button>

      </td>
    </tr>
  </table>
</template>
<script>
import TheHeader from "./TheHeader.vue";
import axios from "axios";
export default {
  name: "HomePage",
  components: {
    TheHeader,
  },
  data() {
    return {
      name: "",
      restaurant: [],
    };
  },
  async mounted() {
   this.loadDate();
  },
  methods:{
    async deleteRes(id){
    let result=await axios.delete("http://localhost:3000/restaurant/"+id)
    if(result.status===200)
    {
       this.loadDate(); 
    }
    },
    async loadDate(){
    let user = localStorage.getItem("user-info");
    this.name = JSON.parse(user).name;
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
    let result = await axios.get("http://localhost:3000/restaurant");
    this.restaurant = result.data;
    }
  }
};
</script>

<style scoped>
td {
  width: 160px;
  height: 40px;
}
</style>
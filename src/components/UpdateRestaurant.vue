<template>
  <the-header> </the-header>
  <h1>Hey {{name}}, Update Restaurant</h1>
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
    <button type="button" v-on:click="updateRestaurant">Update Restaurant</button>
  </form>
</template>
<script>
import TheHeader from "./TheHeader.vue";
import axios from 'axios'

export default {
  name: "UpdateRestaurant",
  components: {
    TheHeader,
  },
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  async mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
    const result=await axios.get('http://localhost:3000/restaurant/'+this.$route.params.id)
    console.log(result.data);
    this.restaurant=result.data;
  },
  methods:{
    async updateRestaurant(){
    const result=await axios.put("http://localhost:3000/restaurant/"+this.$route.params.id,
      {
      name:this.restaurant.name,
      address:this.restaurant.address,
      contact:this.restaurant.contact
      })
      if(result.status==200)
      {
        this.$router.push({name:'HomePage'})
      }
      console.log(result)
    },
    }
  
};
</script>
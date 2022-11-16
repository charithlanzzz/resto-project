<template>
  
  <Header />
  <h1>Hello {{ name }}, welcome to home page</h1>
  <table class="table table-dark table-striped">
    <thead>
    <tr>
      <td>ID</td>
      <td>Name</td>
      <td>Contact</td>
      <td>Address</td>
      <td>Action</td>
    </tr>
    </thead>
    <tbody>
    <tr v-for="item in restaurant" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.contact }}</td>
      <td>{{ item.address }}</td>
      <td>
        <router-link :to="'/update/' + item.id" class="btn btn-success">Update</router-link>
        <button v-on:click="deleteRestaurant(item.id)" class="btn btn-danger">Delete</button>
      </td>
    </tr>
    </tbody>
  </table>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Home",

  data() {
    return {
      name: "",
      restaurant: [],
    };
  },
  components: {
    Header,
  },

  methods: {
    async deleteRestaurant(id) {
      let result = await axios.delete("http://localhost:3000/restaurant/"+id);
      if (result.status == 200) {
        this.loadData();
      }
    },

    async loadData() {
      let user = localStorage.getItem("user-info");
      this.name = JSON.parse(user).name;
      if (!user) {
        this.$router.push({ name: "SignUp" });
      }

      let result = await axios.get("http://localhost:3000/restaurant");
      this.restaurant = result.data;
    },
  },
  async mounted() {
    this.loadData();
  },
};
</script>
<style>
td {
  width: 160px;
  height: 40px;
}
</style>

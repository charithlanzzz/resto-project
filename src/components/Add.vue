<template>
  <Header />
  <h1>Hello user, welcome to add user page</h1>

  <form class="add">
    <input
      type="text"
      name="name"
      placeholder="Enter the name"
      v-model="restaurant.name"
    />
    <input
      type="text"
      name="address"
      placeholder="Enter the address"
      v-model="restaurant.address"
    />
    <input
      type="text"
      name="contact"
      placeholder="Enter the contact"
      v-model="restaurant.contact"
    />
    <button type="button" v-on:click="addRestaurant">Add New restaurant</button>
  </form>
</template>

<script>
import Header from "./Header.vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Add",
  components: {
    Header,
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
  methods: {
    addRestaurant(){
        console.warn(this.restaurant);
    }
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>

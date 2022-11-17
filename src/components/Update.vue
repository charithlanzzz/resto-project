<template>
    <Header/>
    <h1>Hello user, welcome to update page</h1>





    
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
    <button type="button" v-on:click="updateRestaurant" class="btn btn-success">Update restaurant</button>
  </form>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default{
    // eslint-disable-next-line vue/multi-word-component-names
    name:'Update',
    components:{
        Header
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
    async updateRestaurant(){
        console.warn(this.restaurant);
        const result = await axios.put('http://localhost:3000/restaurant/'+this.$route.params.id,{
            name:this.restaurant.name,
            address:this.restaurant.address,
            contact:this.restaurant.contact
        })
        if(result.status==200)
            {
    
               this.$router.push({name:'Home'})
            }
            console.warn("result",result);
    }
  },


   async mounted()
    {
        let user = localStorage.getItem('user-info');
        if(!user)
        {
            this.$router.push({name:'SignUp'})
        }

        const result = await axios .get('http://localhost:3000/restaurant/'+this.$route.params.id)
       // console.warn(this.$route.params.id)

        this.restaurant = result.data
    }
}
</script>
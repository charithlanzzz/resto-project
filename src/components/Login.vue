<template>
    <img alt="SignUp" src="../assets/restu.png" style="width:110px;height:100px;"> 
    <h1>Login</h1>
    <div class="login">
        <label>Email:</label>
        <input type="text" v-model="email" placeholder="Enter the email"/><br>

        <label>Password:</label><br>
        <input type="text" v-model="password" placeholder="Enter the password"/><br>

        <button v-on:click="login">Login</button>
        <p>
            <router-link to="/sign-up">Sign Up</router-link>
        </p>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name:'Login',

    data()
    {
        return {
            email:'',
            password:''
        }
    },


    methods:{
       async login()
        {
            let result = await axios.get(
                `http://localhost:3000/user?email=${this.email}&password=${this.password}`
            )

            if(result.status==200 && result.data.length>0)
            {
        
               localStorage.setItem("user-info",JSON.stringify(result.data[0]))
               this.$router.push({name:'Home'})
            }

            console.warn(result)
        }
    },

    mounted()
    {
        let user = localStorage.getItem('user-info');
        if(user)
        {
            this.$router.push({name:'Home'})
        }
    }
}
</script>
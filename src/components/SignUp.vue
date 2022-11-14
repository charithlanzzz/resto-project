<template>
   <img alt="SignUp" src="../assets/restu.png" style="width:110px;height:100px;"> 
    <h1>Sign Up</h1>
    <div class="register">
        <label>Name:</label>
        <input type="text" v-model="name" placeholder="Enter the name"/><br>

        <label>Email:</label>
        <input type="text" v-model="email" placeholder="Enter the email"/><br>

        <label>Password:</label><br>
        <input type="text" v-model="password" placeholder="Enter the password"/><br>

        <button v-on:click="signUp" type="submit">Sign Up</button>
    </div>
</template>
<script>
import axios from 'axios'

export default{
    name:'SignUp',
    data()
    {
        return{
            name:'',
            email:'',
            password:'',
        }
    },
    methods:{
        async signUp()
        {
            let result = await axios.post("http://localhost:3000/user",{
                name:this.name,
                email:this.email,
                password:this.password
            });

            console.warn(result);
            if(result.status==201)
            {
        
               localStorage.setItem("user-info",JSON.stringify(result.data))
               this.$router.push({name:'Home'})
            }
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
<style>
.register input 
{
   width: 300px;
   height: 40px;
   padding-left: 20px;
   display: block;
   margin-bottom: 30px;
   margin-right: auto;
   margin-left: auto;
   border: 1px solid skyblue;
}

.register label
{
    margin-left:-250px;
}

.register button
{
   width:200px;
   height:40px;
   border: 1px solid skyblue;
}

</style>
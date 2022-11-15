<template>
    <Header />
    <h1>Hello user, welcome to update page</h1>
</template>

<script>
import Header from './Header.vue'
export default{
    // eslint-disable-next-line vue/multi-word-component-names
    name:'Update',
    components:{
        Header
    },

    mounted()
    {
        let user = localStorage.getItem('user-info');
        if(!user)
        {
            this.$router.push({name:'SignUp'})
        }
    }
}
</script>
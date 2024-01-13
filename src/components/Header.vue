<template>
    <div class="nav">
        <router-link to="/"> Home </router-link> 
        <router-link to="add"> Add Restaurant </router-link> 
        <router-link to="update"> Update Restaurant </router-link> 
        <a v-on:click="logout" href="#"> Logout </a>
    </div>
</template>
<script>
export default {
    name: "Header",
    methods: {
        logout(){
            localStorage.clear();
            this.$router.push({name: 'Login'})
        }
    },
}
</script>
<style>
.nav{
    background-color: green;
    overflow: hidden;
    margin-bottom: 15px;
}
.nav a{
    float: left;
    color: #e0e0e0;
    padding: 14px 16px;
    text-align: center;
    font-size: 17px;
    text-decoration: none;
    margin-right: 5px;
}
.nav a:hover{
    color: white;
    background-color: #07931b;
}
    
</style>
<template>
    <Header />
    <div>
        <h1> Hello {{ name }}, welcome to my home page.</h1>
        <table border="1">
            <thead>
                <tr>
                    <th>No</th>
                    <th>Name</th>
                    <th>Address</th>
                    <th>Contact</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="r in restaurants" :key="r.id">
                    <td>{{r.id}}</td>
                    <td>{{r.name}}</td>
                    <td>{{r.address}}</td>
                    <td>{{r.contact}}</td>
                    <td>
                        <router-link :to="'/update/'+r.id">Update</router-link> | 
                        <button type="button" v-on:click="deleteRestaurant(r.id)"> Delete </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
    name : "HomePage",
    
    data() {
        return {
            name: '',
            restaurants: []
        }
    },
    components: {
        Header
    },
    methods: {
        async deleteRestaurant(id){
            let result = await axios.delete('http://localhost:3000/restaurant/'+id)
            if(result.status == 200){
                this.loadData()
            }
        },

        async loadData(){
            
            let user = localStorage.getItem("user-info")
            this.name = JSON.parse(user).name
            if(!user){
                this.$router.push({name: 'SignUp'})
            }
            let result = await axios.get('http://localhost:3000/restaurant')
            this.restaurants = result.data
        }
    },
    mounted() {
        this.loadData()
        
    },
}
</script>
<style>
    td{
        width: 160px;
        height: 40px;
    }
</style>
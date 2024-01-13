<template>
    <Header />
    <div>
        <h1>Add new restaurant</h1>
        <form class="register">
            <input type="text" v-model="restaurant.name" placeholder="Enter Name">
            <input type="text" v-model="restaurant.address" placeholder="Enter Address">
            <input type="text" v-model="restaurant.contact" placeholder="Enter Contact">
            <button type="button" v-on:click="addRestaurant">Add restaurant</button>
           
        </form>
    </div>
</template>
<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
    name : "Add",
    data() {
        return {
            restaurant: {
                name: '',
                address: '',
                contact: ''
            }
        }
    },
    components: {
        Header
    },
    methods: {
        async addRestaurant(){
            let result = await axios.post('http://localhost:3000/restaurant', {
                name: this.restaurant.name,
                address: this.restaurant.address,
                contact: this.restaurant.contact
            })

            if (result.status == 201) {
                this.$router.push({name: 'HomePage'})
            }

            console.log(result)
        }
    },
}
</script>
<style>
    
</style>
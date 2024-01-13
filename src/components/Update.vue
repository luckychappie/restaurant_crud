<template>
    <Header />
    <div>
        <h1>Update restaurant</h1>
        <form class="register">
            <input type="text" v-model="restaurant.name" placeholder="Enter Name">
            <input type="text" v-model="restaurant.address" placeholder="Enter Address">
            <input type="text" v-model="restaurant.contact" placeholder="Enter Contact">
            <button type="button" v-on:click="updateRestaurant">Update restaurant</button>
           
        </form>
    </div>
</template>
<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
    name : "Update",
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
        async updateRestaurant(){
            let result = await axios.put('http://localhost:3000/restaurant/'+this.restaurant.id, {
                name: this.restaurant.name,
                address: this.restaurant.address,
                contact: this.restaurant.contact
            })

            if (result.status == 200) {
                this.$router.push({name: 'HomePage'})
            }

            console.log(result)
        }
    },
    async mounted() {
        let result = await axios.get(`http://localhost:3000/restaurant/${this.$route.params.id}`)
        this.restaurant = result.data

    },
}
</script>
<style>
    
</style>
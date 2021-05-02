<template>
  <div class="container">
    <!-- <header class="jumbotron"> -->
      <!-- <h3>{{content}}</h3> -->

    <!-- </header> -->
      <Navbar/>
  </div>
</template>

<script>
import UserService from '../services/user.service';
import Navbar from '../components/Navbar.vue'

export default {

  name: 'Admin',
  components:{
    Navbar
  },
  data() {
    return {
      content: '',
      campaigns: [
        { id: 0, title: "Adidas Shoes", description: "Advertisement for Shoes"},
        { id: 1, title: "Nike Shoes", description: "Advertisement for Clothings"},
        { id: 2, title: "Ascis Shoes", description: "Advertisement for Shoes"},
      ]
    };
  },
  mounted() {
    UserService.getAdminBoard().then(
      response => {
        this.content = response.data;
      },
      error => {
        this.content =
          (error.response && error.response.data && error.response.data.message) ||
          error.message ||
          error.toString();
      }
    );
  }
};
</script>

<style>


</style>

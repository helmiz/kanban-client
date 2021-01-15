<template>
  <div>
    <navbar></navbar>
    <form-login v-if="currentPage === 'login'" @check-login="checkLogin"></form-login>  
    <form-register v-else-if="currentPage === 'register'"></form-register>
    <dashboard v-else-if="currentPage === 'dashboard'" :categories = "categories" @addTask="formAddTask"></dashboard>
  </div>
</template>

<script>
import axios from "axios";
import Swal from 'sweetalert2';
import FormLogin from './components/FormLogin.vue';
import FormRegister from './components/FormRegister.vue';
import Navbar from './components/Navbar.vue';
import Dashboard from './components/Dashboard.vue';

export default {
  name: "App",
  data() {
    return {
      currentPage: "login",
      url: 'http://localhost:3000',
      categories: []
    };
  },
  components: {
    FormLogin,
    FormRegister,
    Navbar,
    Dashboard
  },
  methods: {
    checkAuthentication(){
      if (localStorage.access_token) {
        this.fetchCategories()
        this.currentPage = "dashboard"
      } else {
        this.currentPage = "login"
      }
    },
    checkLogin(dataLogin) {
      axios({
        method: "POST",
        url: this.url + "/login",
        data: {
          email: dataLogin.email,
          password: dataLogin.password
        }
      })
        .then(response => {
          console.log(response);
          localStorage.setItem("access_token", response.data.access_token)
        })
        .catch(err => {
          console.log(err);
        })
    },
    fetchCategories(){
      axios({
        method: "GET",
        url: this.url + "/categories",
        headers: {
          access_token: localStorage.access_token
        }
      })
        .then(response => {
          this.categories = response.data
        })
        .catch(err => {
          console.log(err);
        })
    },
    formAddTask(dataTask){
      console.log(dataTask);
      axios({
        method: "POST",
        url: this.url + "/tasks",
        data: {
          CategoryId: dataTask.CategoryId,
          title: dataTask.title
        },
        headers: {
          access_token: localStorage.access_token
        }
      })
        .then(response => {
          this.categories.push(response.data)
          this.fetchCategories()
        })
        .catch(err => {
          console.log(err)
        })
    }
  },
  created(){
    this.checkAuthentication()
  }
};
</script>

<style></style>

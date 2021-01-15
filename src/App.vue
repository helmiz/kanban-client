<template>
  <div>
    <navbar @logoutPage="logoutPage" :token_nav="token_nav"></navbar>
    <form-login v-if="currentPage === 'login'" @check-login="checkLogin" @loginGoogle="loginGoogle" @userRegister="userRegister"></form-login>  
    <form-register v-else-if="currentPage === 'register'"></form-register>
    <dashboard v-else-if="currentPage === 'dashboard'" :categories = "categories" @newTask="generateNewTask" @updatedTask="updatedTask" @deleteTask="deleteTask"></dashboard>
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
      categories: [],
      token_nav: localStorage.access_token
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
        this.token_nav = localStorage.access_token
      } else {
        this.currentPage = "login"
        this.token_nav = ""
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
          localStorage.setItem("access_token", response.data.access_token)
          this.checkAuthentication()
        })
        .catch(err => {
          console.log(err.response.data);
          Swal.fire({
            title: err.response.data.Error,
            text: err.response.data.message,
            icon: 'error',
            confirmButtonText: 'Continue'
          })
        })
    },
    loginGoogle(idToken){
      // console.log(idToken, "GET DARI APP.VUE");
      axios({
        method: "POST",
        url: this.url + "/googleLogin",
        data: {
          id_token: idToken
        }
      })
        .then(response => {
          console.log(response, "RESPOSNE");
          localStorage.setItem("access_token", response.data.access_token)
          this.checkAuthentication()
        })
        .catch(err => {
          Swal.fire({
            title: err.response.data.Error,
            text: err.response.data.message,
            icon: 'error',
            confirmButtonText: 'Continue'
          })
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
          Swal.fire({
            title: err.response.data.Error,
            text: err.response.data.message,
            icon: 'error',
            confirmButtonText: 'Continue'
          })
        })
    },
    generateNewTask(dataTask){
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
          Swal.fire({
            title: err.response.data.Error,
            text: err.response.data.message,
            icon: 'error',
            confirmButtonText: 'Continue'
          })
        })
    },
    updatedTask(dataUpdatedTask){
      axios({
        method: "PUT",
        url: this.url + "/tasks/" + dataUpdatedTask.id,
        data: {
          title: dataUpdatedTask.title,
          CategoryId: dataUpdatedTask.CategoryId
        },
        headers: {
          access_token: localStorage.access_token
        }
      })
        .then(response => {
          this.fetchCategories()
        })
        .catch(err => {
          console.log(err);
          Swal.fire({
            title: err.response.data.Error,
            text: err.response.data.message,
            icon: 'error',
            confirmButtonText: 'Continue'
          })
        })
    },
    deleteTask(deletedTaskId){
      axios({
        method: "DELETE",
        url: this.url + "/tasks/" + deletedTaskId.id,
        headers: {
          access_token: localStorage.access_token
        }
      })
        .then(response => {
          this.fetchCategories()
        })
        .catch(err => {
          console.log(err);
          Swal.fire({
            title: err.response.data.Error,
            text: err.response.data.message,
            icon: 'error',
            confirmButtonText: 'Continue'
          })
        })
    },
    logoutPage(){
      this.checkAuthentication()
    },
    userRegister(dataRegister){
      axios({
        method: "POST",
        url: this.url + "/register",
        data: {
          name: dataRegister.name,
          email: dataRegister.email,
          password: dataRegister.password
        }
      })
        .then(response => {
          this.checkAuthentication()
          this.currentPage = "login"
        })
        .catch(err => {
          console.log(err);
          Swal.fire({
            title: err.response.data.Error,
            text: err.response.data.message,
            icon: 'error',
            confirmButtonText: 'Continue'
          })
        })
      
    }
  },
  created(){
    this.checkAuthentication()
  }
};
</script>

<style></style>

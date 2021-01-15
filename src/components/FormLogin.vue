<template>
  <!-- Login Page - Register Page - Front Page -->
  <div class="container">
    <div class="row">
      <div class="col-sm">
        <div class="container">
          <h1>KANBAN</h1>
        </div>
        <div class="container" id="weatherApi">
          <!-- Gambar -->
        </div>
      </div>
      <div class="col-sm">
        
        <div class="container" id="login-page" v-show="!showRegisterLogin">
          <h2>Login</h2>
          <form @submit.prevent="submitLogin">
            <div class="mb-3">
              <label for="email" class="form-label">Email address</label>
              <input type="email" v-model="email" class="form-control" id="email" aria-describedby="emailHelp" name="email">
            </div>
            <div class="mb-3">
              <label for="password" class="form-label">Password</label>
              <input type="password" v-model="password" class="form-control" id="password" name="password">
            </div>
            <button type="submit" class="btn btn-primary" id="login-btn">Submit</button>
          </form>
            <button class="btn btn-primary" id="registerHere-btn" @click="showRegister()" >Register Here</button> <br> <br>
            <button v-google-signin-button="clientId" class="google-signin-button"> Continue with Google</button>
        </div>
            <form-register v-show="showRegisterLogin" @showLoginPage="showLoginPage" @userRegister="userRegister"></form-register>


      </div>
    </div>
  </div>
</template>

<script>
import GoogleSignInButton from 'vue-google-signin-button-directive'
import FormRegister from './FormRegister.vue';

export default {
  components: { FormRegister },
  name: "FormLogin",
  directives: {
    GoogleSignInButton
  },
  data() {
    return {
      email: "",
      password: "",
      clientId: "877379989129-e1e5mrpnvmdr16n66b47aubpbcvp3c9d.apps.googleusercontent.com",
      showRegisterLogin: false
    }
  },
  methods: {
    submitLogin() {
      const dataLogin = { email: this.email, password: this.password }
      this.$emit('check-login', dataLogin)
      this.password = ""
    },
     OnGoogleAuthSuccess (idToken) {
      // Receive the idToken and make your magic with the backend
      // console.log(idToken, "GET DARI LOGIN FORM")
      return this.$emit('loginGoogle', idToken)
    },
    OnGoogleAuthFail (error) {
      console.log(error)
    },
    showRegister(){
      this.showRegisterLogin = !this.showRegisterLogin
      this.password = ""
    },
    showLoginPage(){
      this.showRegisterLogin= false
      this.password = ""
    },
    userRegister(dataRegister){
      return this.$emit('userRegister', dataRegister)
    }
  }
};
</script>

<style>
.google-signin-button {
  color: white;
  background-color: red;
  height: 50px;
  font-size: 16px;
  border-radius: 10px;
  padding: 10px 20px 25px 20px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

</style>

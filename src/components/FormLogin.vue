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
        
        <div class="container" id="login-page">
          <h2>Login</h2>
          <form @submit.prevent="submitLogin">
            <div class="mb-3">
              <label for="email" class="form-label">Email address</label>
              <input type="email" v-model="email" class="form-control" id="email" aria-describedby="emailHelp" name="email">
              <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
            </div>
            <div class="mb-3">
              <label for="password" class="form-label">Password</label>
              <input type="password" v-model="password" class="form-control" id="password" name="password">
            </div>
            <button type="submit" class="btn btn-primary" id="login-btn">Submit</button>
            <button class="btn btn-primary" id="registerHere-btn">Register Here</button> <br> <br>
            <div class="g-signin2" data-onsuccess="onSignIn"></div>
          </form>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormLogin",
  data() {
    return {
      email: "",
      password: ""
    }
  },
  methods: {
    submitLogin() {
      const dataLogin = { email: this.email, password: this.password }
      return this.$emit('check-login', dataLogin)
    }
  }
};
</script>

<style></style>

<template>
  <div class="container" id="register-page">
    <h2>Register</h2>
    <form @submit.prevent="submitRegister">
      <div class="mb-3">
        <label for="nameRegister" class="form-label">Name</label>
        <input type="text" v-model="name" class="form-control" id="nameRegister" aria-describedby="textHelp"
          name="nameRegister">
      </div>
      <div class="mb-3">
        <label for="emailRegister" class="form-label">Email address</label>
        <input type="email" v-model="email" class="form-control" id="emailRegister" aria-describedby="emailHelp"
          name="emailRegister">
      </div>
      <div class="mb-3">
        <label for="passwordRegister" class="form-label">Password</label>
        <input type="password" v-model="password" class="form-control" id="passwordRegister" name="passwordRegister">
      </div>
      <button type="submit" class="btn btn-primary" id="register-btn">Submit</button>
    </form>
      <button class="btn btn-primary" id="loginHere-btn" @click="showLogin" >Login Here</button> <br> <br>
  </div>
</template>

<script>
export default {
  name: "FormRegister",
  data(){
    return {
      email: "",
      password: "",
      name: ""
    }
  },
  methods: {
    submitRegister() {
      const dataRegister = { name: this.name, email: this.email, password: this.password }
      this.$emit('userRegister', dataRegister)
      this.showLogin()
    },
    showLogin(){
      return this.$emit('showLoginPage')
      this.password = ""
    }
  }
}
</script>

<style>

</style>
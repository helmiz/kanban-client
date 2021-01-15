<template>
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

        <div class="container" id="register-page">
          <h2>Register</h2>
          <form>
            <div class="mb-3">
              <label for="emailRegister" class="form-label">Email address</label>
              <input type="email" class="form-control" id="emailRegister" aria-describedby="emailHelp"
                name="emailRegister">
              <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
            </div>
            <div class="mb-3">
              <label for="passwordRegister" class="form-label">Password</label>
              <input type="password" class="form-control" id="passwordRegister" name="passwordRegister">
            </div>
            <button type="submit" class="btn btn-primary" id="register-btn">Submit</button>
            <button class="btn btn-primary" id="loginHere-btn">Login Here</button> <br> <br>
          </form>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormRegister"
}
</script>

<style>

</style>
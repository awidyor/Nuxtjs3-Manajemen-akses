<template>
<div class="container my-5">
    <div class="row justify-content-center">
      <div class="col-md-4 mt-5">
        <div class="card" style="margin-top: 100px;">
          <div class="card-body text-center shadow">
            <div class="logo">
              <img src="~/assets/images/logoasdp.png" alt="Logo" class="img-fluid">
            </div>
            <div class="login-container mt-4">
              <h4 class="mb-4">E-OFFICE LOGIN</h4>
              <form id="login-form">
                <div class="mb-3">
                  <i class="bi bi-person icon"></i>
                  <input type="text" id="username" class="form-control" required placeholder="Username">
                </div>
                <div class="mb-3">
                  <i class="bi bi-lock icon"></i>
                  <input type="password" id="password" class="form-control" required placeholder="Password">
                  <i class="bi bi-eye" id="show-password-toggle"></i>
                </div>

                <button class="btn btn-primary btn-block" @click="login">Login</button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  methods: {
    async login() {
      try {
        const username = document.getElementById('username').value;
        const password = document.getElementById('password').value;

        // Ganti URL sesuai dengan kebutuhan Anda
        const apiUrl = 'http://localhost:3007/login';

        const response = await axios.post(apiUrl, {
          username,
          password,
        });

        // Lakukan sesuatu dengan data respons jika diperlukan
        console.log(response.data);

        // Contoh: Pindah ke halaman setelah login
        this.$router.push('/reporting');
      } catch (error) {
        // Tangani kesalahan jika terjadi
        console.error('Error during login:', error);
      }
    },
  },
};
</script>

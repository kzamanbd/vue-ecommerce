<template class="hold-transition login-page">
<div class="row">
    <div class="container">
        <div class="col-md-6 offset-md-3 justify-content-center">
            <div class="login-box">
  <div class="login-logo">
    <a href="../../index2.html"><b>Admin</b>LTE</a>
  </div>
  <!-- /.login-logo -->
  <div class="card">
    <div class="card-body login-card-body">
      <p class="login-box-msg">Sign in to start your session</p>

      <form @submit.prevent="login">
        <div class="input-group mb-3">
          <input type="text" class="form-control" placeholder="name" v-model="auth.name">
          <div class="input-group-append">
            <div class="input-group-text">
              <span class="fas fa-envelope"></span>
            </div>
          </div>
        </div>
        <div class="input-group mb-3">
          <input type="password" class="form-control" placeholder="Password" v-model="auth.password" >
          <div class="input-group-append">
            <div class="input-group-text">
              <span class="fas fa-lock"></span>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-8">
            <div class="icheck-primary">
              <input type="checkbox" id="remember">
              <label for="remember">
                Remember Me
              </label>
            </div>
          </div>
          <!-- /.col -->
          <div class="col-4">
            <button type="submit" class="btn btn-primary btn-block">Sign In</button>
          </div>
          <!-- /.col -->
        </div>
      </form>

      <div class="social-auth-links text-center mb-3">
        <p>- OR -</p>
        <a href="#" class="btn btn-block btn-primary">
          <i class="fab fa-facebook mr-2"></i> Sign in using Facebook
        </a>
        <a href="#" class="btn btn-block btn-danger">
          <i class="fab fa-google-plus mr-2"></i> Sign in using Google+
        </a>
      </div>
      <!-- /.social-auth-links -->

      <p class="mb-1">
        <a href="forgot-password.html">I forgot my password</a>
      </p>
      <p class="mb-0">
        <a href="register.html" class="text-center">Register a new membership</a>
      </p>
    </div>
    <!-- /.login-card-body -->
  </div>
</div>
        </div>
    </div>
</div>

<!-- /.login-box -->
</template>

<style scoped>
.login-box, .register-box {
	width: 65%;
	margin: 0 auto;
}
</style>

<script>
    import router from '../router'
import axios from 'axios';

    export default {
        name: 'Login',
        data() {
            return {
                auth: { name: '', password: '' },
            }

        },
        methods: {
        login(){
        let credentials = this.auth;
        
        axios.post('/api/token/', {
            username: credentials.name,
            password: credentials.password
        })
        .then(function (response) {
           router.push({name: "Home"})
            console.log(response);
            window.localStorage.setItem('Ragaccesstoken', response.data.access);
            window.localStorage.setItem('Ragrefreshtoken', response.data.refresh);
            window.localStorage.setItem('RagloggedIn', 'true');
        })
        .catch(function (error) {
            console.log(error);
        });
        

      }
        }


    }
</script>
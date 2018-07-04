<template>
  <div>
      <h1 class="text-center mt-5">Stuck Overflow™</h1>
      <div class="container pt-3">
        <div class="row justify-content-sm-center">
          <div class="col-sm-10 col-md-6">
            <div class="card border-info">
              <div class="card-header">Sign in to continue</div>
              <div class="card-body">
                <div class="row">
                  <div class="col-md-4 text-center">
                    <img src="https://placeimg.com/128/128/tech/sepia" class="mb-2">
                  </div>
                  <div class="col-md-8">
                    <form class="form-signin">
                      <input type="text" class="form-control mb-2" placeholder="Email" required autofocus v-model="username">
                      <input type="password" class="form-control mb-2" placeholder="Password" required v-model="password">
                      <button class="btn btn-lg btn-primary btn-block mb-1" @click="fiturLogin()">Sign in</button>
                      <label class="checkbox float-left">
                    <input type="checkbox" value="remember-me">
                    Remember me
                  </label>
                    </form>
                  </div>
                </div>
              </div>
            </div>
            <router-link :to="{ name: 'signup' }">Create an account</router-link>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import sweetalert from 'sweetalert'

  export default {
    data(){
      return{
        username:'',
        password:'',
      }
    },
    methods:{
      fiturLogin: function(){
        let userLogin = {
          email : this.username,
          password : this.password
        }
        axios.post('http://localhost:3000/users/login',userLogin)
        .then((userToken) => {
          swal("Good job!", "You already logged in!", "success");
          localStorage.setItem('token',userToken.data.token)
          localStorage.setItem('userId',userToken.data.userId)
          localStorage.setItem('status',true)
          this.$router.push('/')
        })
        .catch((err) => {
          console.log(err);
        })
      },
      toRegister:function(){
        this.$router.push('/register')
      }
    }
  }
</script>

<style>
</style>

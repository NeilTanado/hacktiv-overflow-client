<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarTogglerDemo03" aria-controls="navbarTogglerDemo03" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <router-link class="navbar-brand" :to="{ name: 'home' }">Nanya Pake Flow!</router-link>
      <div class="collapse navbar-collapse" id="navbarTogglerDemo03">
        <ul class="navbar-nav mr-auto mt-2 mt-lg-0">
          <li class="nav-item active">
            <router-link class="nav-link" :to="{ name: 'home' }">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" :to="{ name: 'about' }">About</router-link>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <div v-if="isLogin">
            <button class="btn btn-outline-light my-2 my-sm-0 mr-3" @click="toQuestion()" ><b>Make Question</b></button>
            <button class="btn btn-outline-warning my-2 my-sm-0 mr-3" @click="toLogout()"><b>Logout</b></button>
          </div>
          <div v-else>
            <button class="btn btn-outline-warning my-2 my-sm-0 mr-3" @click="toLogin()"><b>Login</b></button>
          </div>
        </form>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  data(){
    return{
      isLogin : false
    }
  },
  methods:{
    toLogin(){
      this.$router.push('/signin')
    },
    toLogout(){
      localStorage.clear()
      this.$router.push('/')
      this.cekLogin()
    },
    toQuestion(){
      this.$router.push('/question')
    },
    cekLogin(){
      if(localStorage.getItem('status')){
        this.isLogin = true
      }else{
        this.isLogin = false
      }
    }
  },
  created(){
    this.cekLogin()
  }
}
</script>

<style lang="css">
</style>

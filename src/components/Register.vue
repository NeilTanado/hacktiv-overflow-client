<template>
  <div class="container-fluid py-3">
    <div class="row">
      <div class="col-md-6 mx-auto">
        <div class="card card-body">
          <h3 class="text-center mb-4">Sign-up</h3>
            <fieldset>
              <div class="form-group has-error">
                  <input class="form-control input-lg" placeholder="E-mail Address" v-model="email" type="text">
              </div>
              <div class="form-group has-error">
                  <input class="form-control input-lg" placeholder="Your Name Here" v-model="name" type="text">
              </div>
              <div class="form-group has-success">
                  <input class="form-control input-lg" placeholder="Password" v-model="password" value="" type="password">
              </div>
              <div class="checkbox">
                  <label class="small">
                      <input name="terms" type="checkbox">I have read and agree to the <a href="#">terms of service</a>
                  </label>
              </div>
              <button class="btn btn-lg btn-primary btn-block" @click="register()">Sign Me Up</button>
          </fieldset>
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
      name:'',
      email:'',
      password:''
    }
  },
  methods:{
    register:function(){
      axios.post('http://localhost:3000/users/createuser',{
        email: this.email,
        name: this.name,
        password: this.password
      })
      .then((value) => {
        swal("Good job!", "You already registered!", "success");
        this.$router.push('/signin')
      })
      .catch((err) => {
        console.log(err);
      })
    }
  }
}
</script>

<style lang="css">
</style>

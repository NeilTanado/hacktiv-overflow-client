<template>
  <div class="container mt-5">
    <Vueditor ref='editor'></Vueditor>
    <button type="button" class="btn btn-secondary btn-lg btn-block mt-2" @click="ask()">Ask Something</button>
  </div>
</template>

<script>
import axios from 'axios'
import swal from 'sweetalert2'
import Vueditor from 'vueditor'

export default {
  data(){
    return{

    }
  },
  component:{
    Vueditor
  },
  methods:{
    ask(){
      let sent = {question:this.$refs.editor.getContent()}
      let token = localStorage.getItem('token')
      console.log(sent);
      axios.post('http://localhost:3000/questions/createquestion',sent,{
        headers:{
          token
        }
      })
      .then((value) => {
        swal(
          'You just asking other',
          'success'
        )
        this.$router.push('/')
      })
      .catch((err) => {
        console.log(err);
      })
    },
    ngecekLogin(){
      if(localStorage.getItem('token')){

      }else{
        this.$router.push('/')
      }
    }
  },
  created(){
    this.ngecekLogin()
  }
}
</script>

<style lang="css">
</style>

<template>
  <div class="container">
    <div class="card mt-4" v-for="question in questions">
      <div class="card-header">
        Question From <b>{{question.owner.name}}</b>
      </div>
      <div class="card-body">
        <h5 class="card-title">{{question.question}} </h5>
        <p class="card-text">{{question.date}}</p>
        <router-link class="btn btn-primary" :to="{ path: '/answer', query:{id:question._id}}">Read and Help Answer</router-link>
      </div>
    </div>
  </div>
</template>

<script>
import swal from 'sweetalert2'
import axios from 'axios'

export default {
  data(){
    return{
      questions : []
    }
  },
  methods:{
    getData(){
      axios.get('http://localhost:3000/questions/callquestion')
      .then((value) => {
        console.log(value.data.value);
        this.questions = value.data.value.reverse()
      })
      .catch((err) => {
        console.log(err);
      })
    }
  },
  created(){
    this.getData()
  }
}
</script>

<style lang="css">
</style>

<template>
  <div>
    <div class="container mt-5">
      <div class="card">
        <div class="card-header">
          Question
        </div>
        <div class="card-body">
          <blockquote class="blockquote mb-0">
            <p v-html="theQuestion.question"></p>
            <footer class="blockquote-footer">Question by  <cite title="Source Title">{{theQuestion.owner.name}}</cite></footer>
            <button class="btn btn-success mr-4" @click="upvoteQuestion()"><i class="fas fa-thumbs-up"> {{theQuestion.upvote.length}}</i></button>
            <button class="btn btn-danger" @click="downvoteQuestion()"><i class="fas fa-thumbs-down">{{theQuestion.downvote.length}}</i></button>
          </blockquote>
        </div>
      </div>
    </div>
    <div class="container mt-2">
      <Vueditor ref='editor'></Vueditor>
      <button type="button" class="btn btn-secondary btn-lg btn-block mt-2" @click="answer(theQuestion._id)">Help Answer</button>
    </div>
    <div class="container mt-3">
      <div class="row">
        <div class="col-sm-6 mt-2" v-for="(answer,index) in answers">
          <div class="card">
            <div class="card-body">
              <h4 class="card-title" v-html="answer.answer"></h4>
              <h6 class="card-text">answer by : <b>{{answer.name}}</b></h6>
              <p class="card-text">{{answer.date}}</p>
              <button class="btn btn-success mr-4" @click="upvoteAnswer(index,answer._id)"> <i class="fas fa-thumbs-up"> {{answer.upvote.length}}</i></button>
              <button class="btn btn-danger" @click="downvoteAnswer(index,answer._id)"><i class="fas fa-thumbs-down"></i>{{answer.downvote.length}}</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import swal from 'sweetalert2'
import axios from 'axios'
import Vueditor from 'vueditor'

export default {
  component:{
    Vueditor
  },
  data(){
    return{
      questionId : '',
      theQuestion: {},
      answers:[]
    }
  },
  methods:{
    ngecekLogin(){
      if(localStorage.getItem('token')){

      }else{
        this.$router.push('/')
      }
    },

    upvoteQuestion(){
      let token = localStorage.getItem('token')
      let upvote = this.theQuestion.upvote
      let status = false
      for(var i = 0 ; i < upvote.length ; i++){
        if(localStorage.getItem('userId') === upvote[i]){
          status = true
        }
      }
      if(!status){
        axios.put('http://localhost:3000/questions/upvoteQuestion/'+this.questionId,null,{
          headers:{
            token
          }
        })
        .then((value) => {
          this.getData()
          console.log(value);
        })
        .catch((err) => {
          console.log(err);
        })
      }
    },

    downvoteQuestion(){
      let token = localStorage.getItem('token')
      let downvote = this.theQuestion.downvote
      let status = false
      for(var i = 0 ; i < downvote.length ; i++){
        if(localStorage.getItem('userId') === downvote[i]){
          status = true
        }
      }
      if(!status){
        axios.put('http://localhost:3000/questions/downvoteQuestion/'+this.questionId,null,{
          headers:{
            token
          }
        })
        .then((value) => {
          this.getData()
          console.log(value);
        })
        .catch((err) => {
          console.log(err);
        })
      }
    },

    answer(sentId){
      let sent = {answer:this.$refs.editor.getContent(),questionId:sentId}
      let token = localStorage.getItem('token')
      axios.post('http://localhost:3000/questions/createanswer',sent,{
        headers:{
          token
        }
      })
      .then((value) => {
        swal(
          'You just asking other',
          'success'
        )
        this.getData()
      })
      .catch((err) => {
        console.log(err);
      })
    },

    getData(){
      let self = this
      axios.get('http://localhost:3000/questions/onequestion/'+self.questionId)
      .then((value) => {
        this.theQuestion = value.data.value
        this.answers = value.data.value.answer
      })
      .catch((err) => {
        console.log(err);
      })
    },

    upvoteAnswer(i,id){
      let token = localStorage.getItem('token')
      let upvote = this.answers[i].upvote
      let status = false
      for(var i = 0 ; i < upvote.length ; i++){
        if(localStorage.getItem('userId') === upvote[i]){
          status = true
        }
      }
      if(!status){
        axios.put('http://localhost:3000/questions/upvoteAnswer/'+id,null,{
          headers:{
            token
          }
        })
        .then((value) => {
          this.getData()
          console.log(value);
        })
        .catch((err) => {
          console.log(err);
        })
      }
    },

    downvoteAnswer(i,id){
      let token = localStorage.getItem('token')
      let downvote = this.answers[i].downvote
      let status = false
      for(var i = 0 ; i < downvote.length ; i++){
        if(localStorage.getItem('userId') === downvote[i]){
          status = true
        }
      }
      if(!status){
        axios.put('http://localhost:3000/questions/downvoteAnswer/'+id,null,{
          headers:{
            token
          }
        })
        .then((value) => {
          this.getData()
          console.log(value);
        })
        .catch((err) => {
          console.log(err);
        })
      }
    },
  },
  created(){
    this.ngecekLogin()
    this.questionId = this.$route.query.id
    this.getData()
  }
}
</script>

<style lang="css">
</style>

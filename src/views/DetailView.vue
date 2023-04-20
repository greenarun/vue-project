<script>   
import axios from 'axios'
export default {
 data() {
   return { 
     listData: {},
     status:null,
     elementVisible:false
   }
 },
 methods: { 
   async fetchList() {  
    const id = this.$route.params.id;
    this.listData = {}

    axios
    .get(`http://localhost:3000/posts/${id}`)
    .then(response => (this.listData = response.data))
    .catch(error => console.log(error)) 
   },
   async updateVote(){
    const id = this.$route.params.id;

    axios
    .put(`http://localhost:3000/posts/${id}`,this.listData)
    .then(response => (console.log(response),this.elementVisible=true,this.status="voted"))
    .catch(error => console.log(error),this.elementVisible=true,this.status="error")  
    setTimeout(() => this.elementVisible = false, 1000)
   },
   handleIncreament() {
    let vote = this.listData.votes 
    vote=vote+1 
    this.listData.votes = vote
    this.updateVote() 
   },
   handleDecreament(){
    let vote = this.listData.votes 
    vote=vote-1 
    this.listData.votes = vote
    this.updateVote()
   }
 },
 mounted() {
   this.fetchList()
 }
}
   </script>
<template>
  <div class="detail-container">
    <div class="flag" v-show="elementVisible">{{ status }}</div>
  <h2>{{ listData.title }}</h2>
  <div class="detailItem">
    <div class="voting"> 
      <button @click="handleIncreament" class="btnVote">+</button>
      <div class="vote">{{ listData.votes }}</div>
      <button @click="handleDecreament" class="btnVote">-</button> 
    </div>
    <div class="detail"> 
      <div>{{ listData.description }}</div>
    </div> 
  </div>
</div>
  </template>
  
  <style> 
  .detail-container{ 
    width:80%;margin:0 auto;
  }
  .detailItem{display: flex;}
  .vote{text-align: center;margin:10px}
  .voting{padding:10px;background-color: #eee;margin: 10px 10px 0;height: 90px;}
  .detail {  align-items: center; margin:10px } 
  .btnVote{cursor: pointer;}
  .flag{background-color: #ff9797;padding:10px}
  </style>
  
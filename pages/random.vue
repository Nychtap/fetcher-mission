<template>
  <div class="container">
    <div class="box1">
      <div class="h">
        <h3>Random</h3><p  id = "demo" ></p>
      </div>
      <div class="b">
        <button @click="warn()">Random</button>
        <h1 v-if="ok"><i class="fas fa-spinner fa-pulse" />Loading</h1>
      </div>
  </div>
  <div class="box2">
    <div id="but">
      <!-- <h1 v-if="ok">Loading</h1> -->


      <!-- <p>{{ posts }}</p> -->

      <h4>UserID: {{ posts.userId }}</h4>

      <h4>Title: {{ posts.title }}</h4>
      <h4>{{ posts.body }}</h4>

      <!-- <p>{{ comments }}</p> -->
      <!-- <button @click="e('Form cannot be submitted yet.', $event)">e</button> -->
    </div>
  </div>
  <div class="box3">
    <!-- <button @click="warn2()">Comments</button> -->
    <ul v-if="comments && comments.length">
      <li
        v-for="comments of comments"
        :key="comments.name">
        <div class="box_c">
          <p><strong>ID: {{ comments.id }}</strong></p>
          <p>Name: {{ comments.name }}</p>
          <p>Email: {{ comments.email }}</p>
          <p>Comments: {{ comments.body }}</p>
        </div>
      </li>
    </ul>
  </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data(){
    return{
      ok: false,
      d:Number,
      posts: [],
      errors: [],
      comments: [],
    };
  },
  methods: {
   warn() {
     var x = document.getElementById("demo");
     x.innerHTML = Math.floor((Math.random() * 100) + 1);
     this.d =  x.innerHTML;
     setTimeout(() => {this.ok = true;
       axios.get('https://jsonplaceholder.typicode.com/posts/'+ this.d)
         .then((response) => {
           this.posts = response.data;
           console.log(this.posts);
           // this.a = 'found ' + this.posts.length + ' items';
         })
         .catch((e) => {
           this.errors.push(e);
           console.log(this.errors);
           // alert(e);
         });
         axios.get('https://jsonplaceholder.typicode.com/posts/'+ this.d + '/comments')
           .then((response) => {
             setTimeout(() => {this.ok = false;}, 1000);
             this.comments = response.data;
             console.log(this.comments);
             // this.a = 'found ' + this.posts.length + ' items';
           })
           .catch((e) => {
             this.errors.push(e);
             console.log(this.errors);
             // alert(e);
           });}, 1000);
   },
}
};
</script>
<style lang="css">
body{
    margin            : 0;
    padding           : 0;
    /* background-color: #6666ff; */
    background-image: url("C:/Users/NOK/Desktop/fetcher-mission/pages/coffee_cup_minimalism_120197_1600x1200.jpg");
}
.container{

  display           : flex;
  flex-direction    : column;
  width             : 100%;
  height            : 100%;
  justify-content: center;
  /* background-color  : #d9d9d9; */
}
ul{
  list-style-type: none;
}
button{
  background-color: #a36629;
    border: none;
    color: white;
    padding: 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 12px;
    margin: 4px 2px;
    cursor: pointer;
    border-radius: 12px;
}
.box_c{
  margin-top: 2vh;
  margin-left: 2vh;
  margin-right: 2vh;
  width: 80%;
  flex-direction: column;
  background-color: #ebebfa;
  /* color: #6666ff; */
  color: #4d2600;
  font-family:  cursive;
  justify-content: center;
  border          : 1px solid tranparrent;
  opacity         : 0.6;
  filter          : alpha(opacity=60);
}
.b{

  padding: 10px 20px;
  border: 1px solid #ddd;
  color: #333;
  background-color:#fff;
  border-radius: 4px;
  font-size: 14px;
  font-family: arail;
  cursor: pointer;
}
.box3{
  width: 100%;
  height: 40%;
  margin-left: 10%;
  margin-right: 10%;

}
.box2{
  font-size: 1.5em;
  width: 85%;
  margin-left: 10%;
  margin-right: 10%;
  height: 35%;
  /* color: #ebebfa; */
  color: #a36629;
}
.box1{
  flex-direction: column;
  font-size: 3em;
  color: #331a00;
  /* margin-left: 2vh;
  margin-right: 2vh; */
  width: 100%;
  height: 25%;
  background-color: #ebebfa;
  /* background-image: url("C:/Users/NOK/Desktop/fetcher-mission/pages/atmosphere-cloudiness-clouds-844297.jpg"); */
}
</style>
<!-- #ffcc99 -->

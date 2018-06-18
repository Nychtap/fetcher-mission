<template>
  <div class="container">
    <div class="box1">
      <h3>Random</h3>
  </div>
  <div class="box2">
    <div id="but">
      <h1 v-if="ok">Loading</h1>

      <button @click="warn()">Random</button>
      <!-- <p>{{ posts }}</p> -->
      <p  id = "demo" ></p>
      <p>UserID{{ posts.userId }}</p>

      <p>Title{{ posts.title }}</p>
      <p>{{ posts.body }}</p>

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
      // ok: false,
      d:Number,
      posts: [],
      errors: [],
      comments: [],
    };
  },
  methods: {
   // warn2() {
   //
   //   // this.ok = true;
   //
   // },
   warn() {
     var x = document.getElementById("demo");
     x.innerHTML = Math.floor((Math.random() * 100) + 1);
     this.d =  x.innerHTML;
     // this.ok = true;
     axios.get('https://jsonplaceholder.typicode.com/posts/'+ this.d)
       .then((response) => {
         // this.ok = false;
         this.posts = response.data;
         console.log(this.posts);
         // this.a = 'found ' + this.posts.length + ' items';
       })
       .catch((e) => {
         // this.ok = false;
         this.errors.push(e);
         console.log(this.errors);
         // alert(e);
       });
       axios.get('https://jsonplaceholder.typicode.com/posts/'+ this.d + '/comments')
         .then((response) => {
           // this.ok = false;
           this.comments = response.data;
           console.log(this.comments);
           // this.a = 'found ' + this.posts.length + ' items';
         })
         .catch((e) => {
           // this.ok = false;
           this.errors.push(e);
           console.log(this.errors);
           // alert(e);
         });
   },
}
};
</script>
<style lang="css">
body{
    margin            : 0;
    padding           : 0;
    background-color: #6666ff;
}
.container{
  display           : flex;
  flex-direction    : column;
  width             : 100%;
  height            : 100%;
  justify-content: center;
  /* background-color  : #d9d9d9; */
}
.box_c{
  margin-top: 2vh;
  margin-left: 2vh;
  margin-right: 2vh;
  width: 80%;
  flex-direction: column;
  background-color: #ebebfa;
  color: #6666ff;
  font-family:  cursive;
  justify-content: center;
}
</style>
<!-- #ffcc99 -->

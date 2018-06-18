<template>
  <div class="container">
    <div>
      <div id="but">
        <h1 v-if="ok">Loading</h1>
        <button @click="warn('Form cannot be submitted yet.', $event)">Show</button>
        <button @click="e('Form cannot be submitted yet.', $event)">e</button>
      </div>
      <div class="pop">
        <pop :txt="a"/>
    </div>
      <ul v-if="posts && posts.length">
        <li
          v-for="post of posts"
          :key="post.name">
          <p><strong>{{ post.name }}</strong></p>
          <p>{{ post.username }}</p>
          <p>{{ post.email }}</p>
        </li>
      </ul>

  </div>
</div>
</template>

<script>
import axios from 'axios';
import pop from '~/components/pop.vue';
// Import component

export default {
  components:{
    pop,
  },
  data() {
    return {
      ok: false,
      posts: [],
      errors: [],
      a: '',
    };
  },
  methods: {
    e(message, event) {
      this.ok = true;
      // now we have access to the native event
      if (event) event.preventDefault();
      axios.get('https://reqres.in/api/unknown/23')
        .then((response) => {
          this.posts = response.data;
          console.log(this.posts);
        })
        .catch((e) => {
          this.ok = false;
          this.errors.push(e);
          console.log(this.errors);
          alert(e);
          this.a = e.message;
        });
    },
    warn(message, event) {
      this.ok = true;
      // now we have access to the native event
      if (event) event.preventDefault();
      axios.get('https://jsonplaceholder.typicode.com/users')
        .then((response) => {
          this.ok = false;
          this.posts = response.data;
          console.log(this.posts);
          this.a = 'found ' + this.posts.length + ' items';
        })
        .catch((e) => {
          this.ok = false;
          this.errors.push(e);
          console.log(this.errors);
          // alert(e);
        });
    },
  },
};
</script>
<style lang="css">
body{
    margin            : 0;
    padding           : 0;
}
.container-bank {
  display           : flex;
  flex-direction    : row;
  width             : 100%;
  height            : 100%;
  background-color  : #d9d9d9;
}
</style>

<template>
  <div id="app">
    <header>  
      <h1>My page with Vue.js</h1>
    </header>

    <main>
      <aside class="sidebar">
        <router-link
          v-for="post in posts" 
          v-bind:key="post"
          active-class="is-active"
          class="link"
          :to="{name: 'post', params: {id: post.id}}">
            {{post.id}}. {{post.title}}
        </router-link>
      </aside>

      <div class="content">
        <router-view></router-view> 
      </div>   
    </main>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data () {
    return {
      posts: null,
      endpoint: 'https://jsonplaceholder.typicode.com/posts/',
    }
  },

  created () {
    this.getAllPosts();
  },

  methods: {  
    getAllPosts(){
      axios.get(this.endpoint)
        .then(response => {
          this.posts = response.data;
        })
        .catch(error => {
          console.log('--error--');
          console.log(error);
        })
    }
  }
}
</script>

<style lang="scss">
  body {
    margin: 0;
    padding: 0;
  }
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    ::-webkit-scrollbar { width: 3px; height: 3px;}
    ::-webkit-scrollbar-button {  background-color: #666; }
    ::-webkit-scrollbar-track {  background-color: #999;}
    ::-webkit-scrollbar-track-piece { background-color: #ffffff;}
    ::-webkit-scrollbar-thumb { height: 50px; background-color: #666; border-radius: 3px;}
    ::-webkit-scrollbar-corner { background-color: #999;}
    ::-webkit-resizer { background-color: #666;}
  }
  h1, h2 {
    font-weight: normal;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  header {
    position: fixed;
    top: 0;
    width: 100%;
    min-height: 90px;
    border-bottom: 1px solid #42b983;
    text-align: center;
    background: #95f0be;
    color: #fff;
    text-transform: uppercase;
  }
  main {
    display: flex;
    height: calc(100vh - 90px);
    max-width: 1200px;
    margin-top: 90px;
    margin-left: auto;
    margin-right: auto;
    overflow: hidden;
  }
  aside {
    flex: 1 0 30%;
    height: 100%;
    overflow-y: auto;
    width: 30%;
    padding: 50px 30px;
    box-sizing: border-box;
    border-right: 1px solid #42b983;
  }
  .content {
    flex: 1 1 70%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .link {
    display: block;
    text-decoration: none;
    margin-bottom: 10px;
    color: #2c3e50;
    &--home {
      text-transform: uppercase;
      margin-bottom: 30px;
    }
    &.is-active {
      color: #42b983;
    }
  }
</style>
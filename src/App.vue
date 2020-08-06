<template>
  <div id="app">
    
    <Editor v-if="isLogin" :user="userData"></Editor>
    <Home v-if="!isLogin"></Home>

  </div>
</template>

<script>
import Editor from "./components/Editor.vue"
import Home from "./components/Home.vue"

export default {
  name: 'app',
  data () {
    return {
      isLogin: false,
      userData: null
    }
  },

  created: function(){
    firebase.auth().onAuthStateChanged(user => {
      console.log(user);

      if(user) {
        this.userData = user;
        this.isLogin = true;
      } else {
        this.userData = null;
        this.isLogin = false;
      };
    });
  },

  components: {
    Home: Home,
    Editor: Editor
  }
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
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

a {
  color: #42b983;
}
</style>

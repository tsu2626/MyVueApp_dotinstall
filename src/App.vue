<template>
  <div id="app">
    <Home v-if="!isLogin"></Home>
    <ToDo v-if="isLogin"></Todo>
  </div>
</template>

<script>
import ToDo from './components/ToDo'
import Home from './components/Home'

export default {
  name: 'App',
  data() {
    return {
      isLogin: false
    };
  },
  created: function () {
    firebase.auth().onAuthStateChanged(user => {
      console.log(user);
      if (user) {
        this.isLogin = true;
      } else {
        this.isLogin = false;
      };
    });
  },
  components: {
    ToDo: ToDo,
    Home: Home
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

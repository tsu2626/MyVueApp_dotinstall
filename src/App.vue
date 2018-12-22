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

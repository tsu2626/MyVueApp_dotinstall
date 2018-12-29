<template>
  <div class="hello">
    <h1 class=title>
      My Todos
    </h1>
    <span @click="googSignin" class="button is-outlined is-rounded">
      <img src="https://img.icons8.com/color/30/000000/google-logo.png" style="size: 5px">
      　Sign In or Sign Up
    </span>
  </div>
</template>''
<script>
import firebase from 'firebase'

var config = {
        apiKey: "AIzaSyCqXQSo7dhIy7DLTM77AO36TkfeIP7HcM0",
        authDomain: "todoapp-b6529.firebaseapp.com",
        databaseURL: "https://todoapp-b6529.firebaseio.com",
        projectId: "todoapp-b6529",
        storageBucket: "todoapp-b6529.appspot.com",
        messagingSenderId: "362391702616"
      };
      firebase.initializeApp(config);
export default {
  name:'home',
  data () {
    return {

    }
  },
  methods: {
    googSignin() {
      const provider = new firebase.auth.GoogleAuthProvider()
      firebase.auth().signInWithPopup(provider)
        .catch(error => alert(error.message))
        .then(data => {
          alert('login success')
          console.log(data)
        })
    }
  }

}
</script>
<style lang="">
  
</style>
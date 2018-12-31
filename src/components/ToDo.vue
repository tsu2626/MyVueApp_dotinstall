<template>
  <div class="hello">
    <nav>
      <span class="button is-danger small is-rounded" @click="purge">Purge</span>
      <span class="button is-link small is-rounded" @click="signOut">SignOut</span>
    </nav>
    <h1 class=title>
      My Todos
      <span class="is-size-4 has-text-grey">({{ remaining.length }}/{{ todos.length }})</span>
    </h1>
    <form class="field is-grouped" @submit.prevent="addItem">
      <div class="control is-expanded">
        <input class="input is-rounded" type="text" v-model="newItem" placeholder="Title">
        <textarea class="input is-rounded" type="text" v-model="newContent" style="white-space: pre;" placeholder="Todo"></textarea>
      </div>
      <div class="control">
        <input class="button is-info is-rounded" type="submit" value="Add">
        <span @click="saveItems" class="button is-success is-rounded">Save</span>
      </div>
    </form>
    <ul class="todos is-size-5" v-if="todos.length">
      <li v-for="(todo, index) in todos" :key="todo">
        <label class="checkbox">
          <input type="checkbox" v-model="todo.isDone">
        </label>
        <div class="card">
          <head class="card-header">
            <p class="card-header-title">
              <span :class="{done: todo.isDone}">{{ todo.title }}</span>
            </p>
          </head>
          <div class="card-content">
            <div class="content">
              <span :class="{done: todo.isDone}" style="white-space: pre;">{{ todo.content }}</span>
            </div>
          </div>
          <footer class="card-footer">
            <span class="card-footer-item button">Edit</span>
            <span @click="deleteItem(index)" class="card-footer-item button is-danger">Delete</span>
          </footer>
        </div>
        <!-- <span @click="deleteItem(index)" class="delete">[削除]</span> -->
      </li>
    </ul>
    <ul v-else class="subtitle is-size-4">
      <li>Nothing Todos</li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'ToDo',
    newItem: "",
    props: ["user"],
    data () {
      return {
        todos: [],
        components: [],
      }
    },
    created: function () {
      firebase
        .database()
        .ref('todos/' + this.user.uid)
        .once('value')
        .then(result => {
          if (result.val()) {
            this.todos = result.val();
            this.components = result.val();
          }
        })
    },
    methods: {
      addItem: function() {
        this.todos.push({
          title: this.newItem,
          content: this.newContent,
          isDone: false
        })
        this.newItem = ""
      },
      deleteItem: function(index) {
        if(confirm('Are You Sure?')){
          this.todos.splice(index, 1);
        }
      },
      purge: function() {
        if(!confirm('delete finished?')){
          return; //Noを選んだら何もせす返す
        }
        this.todos = this.remaining;
      },
      saveItems: function () {
        alert('Save Success')
        firebase
          .database()
          .ref('todos/' + this.user.uid)
          .set(this.todos);
      },
      signOut: function () {
        console.log('')
        firebase.auth().signOut();
      }
    },
    computed: {
      remaining: function() {
        return this.todos.filter(function(todo) { //dataのtodosを参照し、
          return !todo.isDone; //未チェックのTodoを返す
        })
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
nav {
  padding-bottom: 2%;
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
.hello li > span.done{
  text-decoration: line-through;
  color: dimgrey;
}
.todos {
  padding-top: 2%;
  padding-bottom: 2%;
}
.subtitle {
  padding-top: 3%;
  padding-bottom: 1%;
}
.field {
  max-width: 300px;
  margin: auto;
}
</style>

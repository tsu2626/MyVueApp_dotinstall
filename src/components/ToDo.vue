<template>
  <div class="hello">
    <h1 class=title>
      My Todos
      <span class="is-size-4 has-text-grey">({{ remaining }}/{{ todos.length }})</span>
      <a class="button is-danger small is-rounded" @click="purge">Purge</a>
    </h1>
    <ul class="todos is-size-5" v-if="todos.length">
      <li v-for="(todo, index) in todos" :key="todo">
        <label class="checkbox">
          <input type="checkbox" v-model="todo.isDone">
        </label>
        <span :class="{done: todo.isDone}">{{ todo.title }}</span>
        <span @click="deleteItem(index)" class="delete">[削除]</span>
      </li>
    </ul>
    <ul v-else class="subtitle is-size-4">
      <li>Nothing Todos</li>
    </ul>
    <form class="field is-grouped" @submit.prevent="addItem">
      <div class="control is-expanded">
        <input class="input is-rounded" type="text" v-model="newItem">
      </div>
      <div class="control">
        <input class="button is-info is-rounded" type="submit" value="Add">
      </div>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'ToDo',
    newItem: "",
    data () {
      return {
        todos: [
          {
            title: 'task1',
            isDone: false
          },
          {
            title: 'task2',
            isDone: true
          },
          {
            title: 'task3',
            isDone: true
          }
        ]
      }
    },
    methods: {
      addItem: function() {
        var item = {
          title: this.newItem,
          isDone: false
        };
        this.todos.push(item);
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
        this.todos = this.todos.filter(function(todo) { //yesを選んだら
          return !todo.isDone; //未チェックのTodoを返す
        });
      }
    },
    computed: {
      remaining: function() {
        var items = this.todos.filter(function(todo) { //dataのtodosを参照し、
          return !todo.isDone; //未チェックのTodoを返す
        });
          return items.length; //itemの数　
       }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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

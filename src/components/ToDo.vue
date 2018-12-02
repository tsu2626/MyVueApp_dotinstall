<template>
  <div class="hello">
    <h1 class=title>My Todos</h1>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo">
        {{ todo.title }}
        <span @click="deleteItem(index)" class="delete">[削除]</span>
      </li>
    </ul>
    <form @submit.prevent="addItem">
      <input type="text" v-model="newItem">
      <input type="submit" value="Add">
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
            isDone: false
          },
          {
            title: 'task3',
            isDone: false
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
</style>

<template>
  <div class="hello">
    <h1 class=title>My Todos</h1>
    <ul class="todos" v-if="todos.length">
      <li v-for="(todo, index) in todos" :key="todo">
        <label class="checkbox">
          <input type="checkbox" v-model="todo.isDone">
        </label>
        <span :class="{done: todo.isDone}">{{ todo.title }}</span>
        <span @click="deleteItem(index)" class="delete">[削除]</span>
      </li>
    </ul>
    <ul v-else class="subtitle">
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
  padding: 1%;
}
.field {
  max-width: 300px;
  margin: auto;
}
</style>

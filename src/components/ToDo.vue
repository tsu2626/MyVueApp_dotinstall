<template>
  <div class="hello">
    <h1>My Todos</h1>
    <ul>
      <li v-for="todo in todos" :key="todo">{{ todo }}</li>
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
        'task1',
        'task2',
        'task3'
      ]
    }
  },
  methods: {
    addItem: function() {
      this.todos.push(this.newItem);
      this.newItem = ""
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

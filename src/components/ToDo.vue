<template>
  <div class="hello">
    <h1>My Todos</h1>
    <ul>
      <li v-for="todo in todos" :key="todo">{{ todo }}</li>
    </ul>
    <form action="">
      <input type="text">
      <input type="button" value="Add">
    </form>
  </div>
</template>

<script>
export default {
  name: 'ToDo',
  data () {
    return {
      todos: [
        'task1',
        'task2',
        'task3'
      ]
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

<template>
  <div id="app">
    <h1>Todos</h1>
    <input type="text" v-model="todoName" @keyup.enter="addTodo">
    <ul>
      <li v-for="todo of todos" :key="todo.id">{{ todo.name }}</li>
    </ul>
  </div>
</template>

<script>
import axios from "axios"

const baseURL = "http://localhost:3000/todos"

export default {
  name: 'app',
  data() {
    return {
      todos: [],
      todoName: ''
    };
  },
  async created() {
    try {
      const result = await axios.get(baseURL);

      this.todos = result.data;

    } catch (e) {
      //console.error(e);
    }
  },
methods: {
  async addTodo() {
    const result = await axios.post(baseURL, { name: this.todoName });

    this.todos = [...this.todos, result.data];

    this.todoName = ''
  }
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

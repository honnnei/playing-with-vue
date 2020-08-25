<template>
  <div id="app">
    <Header />
    <router-view/>
  </div>
</template>

<script>
import Axios from 'axios';
import Header from './components/layout/Header.vue';

export default {
  name: 'App',
  components: {
    Header
   
  },
  data() {
    return {
      todos: [
      ]
}
},
methods: {
  deleteTodo(id) {
    Axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
    .then(res => this.todos = this.todos.filter(todo => todo.id !== id, res ))
    .catch(err => console.log(err));
  },
  addTodo(newTodo) {
    const { title, completed } = newTodo;
    Axios.post('https://jsonplaceholder.typicode.com/todos', {
      title,
      completed
    })
    .then(res => this.todos = [...this.todos, res.data])
    .catch(err => console.log(err));
  }},
  created() {
    Axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

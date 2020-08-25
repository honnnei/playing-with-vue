<template>
  <div id="app">
    <AddTodo  v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:delete-todo="deleteTodo" />
    <Form />

  </div>
</template>

<script>
import Form from '../components/Form.vue'
import Todos from '../components/Todos.vue';
import AddTodo from '../components/AddTodo.vue';
import Axios from 'axios';

export default {
  name: 'Home',
  components: {
    Form, 
    Todos, 
    AddTodo
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


<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

import axios from 'axios';
import Todos from "./components/Todos";
import Header from "./components/layout/Header";
import AddTodo from "./components/AddTodo";

export default {
  name: "App",
  created: function(){
      axios.get('http://jsonplaceholder.typicode.com/todos?_limit=4')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err));

  },
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id );
      //this.todos = this.todos.filter(todo => todo.id != id);
      // axios.delete(`http://jsonplaceholder.typicode.com/todos/${id}`)
      //   .then(() => this.todos = this.todos.filter(todo => todo.id !== id))
      //   .catch (err => console.log(err));
    },
    addTodo(newTodo) {
      const {title, completed} = newTodo;
      axios.post('http://jsonplaceholder.typicode.com/todos', {title, completed})
      .then(res => this.todos.push(res.data));
      //this.todos.push(newTodo);
    }
  }
}

</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>



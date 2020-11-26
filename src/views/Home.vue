<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>            
import Todos from '@/components/Todos';
import AddTodo from '@/components/AddTodo';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Todos,
    AddTodo
  },
  data(){
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id){
      //this.todos = this.todos.filter( todo => todo.id !== id)
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then( res => {
        this.todos = this.todos.filter( todo => todo.id !== id );
        return res;
      })
      .catch(error => {
        return Promise.reject(error);
      });
    },
    addTodo(newTodo){
      const { id, title, completed } = newTodo;
      //this.todos = [ ...this.todos, newTodo ];
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        id,
        title,
        completed
      })
      .then( res => this.todos = [ ...this.todos, res.data ])
      .catch(error => {
        return Promise.reject(error);
      });

    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(res => this.todos = res.data)
    .catch(error => {
      return Promise.reject(error);
    })
  }
  
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.btn {
  display: inline; 
  border: none;
  border-radius: 0;
  padding:  8px 20px;
  background: navy;
  color: aliceblue;
  cursor: pointer;
}
.btn:hover {
}
</style>

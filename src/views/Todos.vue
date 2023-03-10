<template>
    <div>
      <h2>Todo application</h2>
      <router-link to="/">Home</router-link>
      <hr>
      <AddTodoItem
        @add-todo-item="addTodoItem"
      />
      <hr>
      <Loader v-if="loading" />
      <TodoList
        v-else-if="todos.length"
        v-bind:todos="todos"
        @remove-item="removeItem"
      />
      <p v-else>No todos!</p>
    </div>
  </template>
  
  <script>
  import TodoList from '@/components/TodoList'
  import AddTodoItem from '@/components/AddTodoItem'
  import Loader from '@/components/Loader'
  export default {
    name: 'App',
    data() {
      return {
        todos: [],
        loading: true
      }
    },
    mounted() {
      fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(response => response.json())
        .then(json => {
          setTimeout(() => {
            this.todos = json
            this.loading = false
          }, 1000)
          
        })
    },
    methods: {
      removeItem(id) {
        this.todos = this.todos.filter(i => i.id !== id)
      },
      addTodoItem(todo) {
        this.todos.push(todo)
      }
    },
    components: {
      TodoList,
      AddTodoItem,
      Loader
    }
  }
  </script>

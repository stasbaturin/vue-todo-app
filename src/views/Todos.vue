<template>
    <div>
      <h2>Todo list</h2>
      <router-link to="/">Home</router-link>
      <hr>
      <AddTodoItem
        @add-todo-item="addTodoItem"
      />
      <select v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not Completed</option>
      </select>
      <hr>
      <Loader v-if="loading" />
      <TodoList
        v-else-if="filteredTodos.length"
        v-bind:todos="filteredTodos"
        @remove-item="removeTodoItem"
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
        loading: true,
        filter: 'all'
      }
    },
    mounted() {
      fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(response => response.json())
        .then(json => {
          setTimeout(() => { // for testing the Loader
            this.todos = json
            this.loading = false
          }, 1000)
          
        })
    },
    watch: { // for testing watch functionality
      filter(value) {
        console.log(value)
      }
    },
    computed: {
      filteredTodos() {
        if (this.filter === 'all') {
          return this.todos
        }
        if (this.filter === 'completed') {
          return this.todos.filter(t => t.completed)
        }
        if (this.filter === 'not-completed') {
          return this.todos.filter(t => !t.completed)
        }
      }
    },
    methods: {
      removeTodoItem(id) {
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

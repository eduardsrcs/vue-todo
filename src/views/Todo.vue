<template>
  <div>
    <h2>ToDos</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo
      @add-todo="addTodo"
    />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <hr>
    <Loader v-if="loading" />
    <TodoList
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>No Todos</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList' // @ means source folder
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'

export default {
  name: 'App',
  data() {
    return ({
      todos: [],
      loading: true,
      filter: 'all'
    })
  },
  // watch: {
  //   filter(value) {
  //     console.log(value)
  //   }
  // },
  computed: {
    filteredTodos() {
      if (this.filter ==='all') {
        return this.todos
      }
      if (this.filter ==='completed') {
        return this.todos.filter((t) => t.completed)
      }
      if (this.filter ==='not-completed') {
        return this.todos.filter((t) => !t.completed)
      }
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=7')
      .then(response => response.json())
      .then(json => {
        this.todos = json
        this.loading = false
        })
  },
  components: {
    TodoList, AddTodo, Loader
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id != id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  }
}
</script>
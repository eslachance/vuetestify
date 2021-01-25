<template>
  <div class="home">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Todos from '../components/Todos.vue'
import AddTodo from '../components/AddTodo.vue'

interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

@Component({
  components: {
    Todos,
    AddTodo
  },
  data () {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo (id: number): void {
      // Squiglies caused by Vetur, no actual problem, ignore for now.
      // The solutions for this either disable features or are just a PITA to implement.
      fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, { method: 'DELETE' })
        .then(() => { this.todos = this.todos.filter(todo => todo.id !== id) })
    },
    addTodo (title) {
      fetch('https://jsonplaceholder.typicode.com/todos', {
        method: 'POST',
        body: JSON.stringify({
          title,
          completed: false
        })
      })
        .then(r => r.json())
        .then(data => { this.todos = [...this.todos, data] })
        .catch(console.error)
    }
  },
  created () {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10').then(r => r.json())
      .then(data => { this.todos = data })
      .catch(console.error)
  }
})
export default class Home extends Vue {}
</script>

<template>
<div>
  <div v-for="todo in todos" v-bind:key="todo.id">
    <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" />
  </div>
</div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
import TodoItem from './TodoItem.vue'

interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

@Component({
  components: {
    TodoItem
  }
})
export default class Todos extends Vue {
  @Prop() private todos!: Array<Todo>
}
</script>

<style scoped>
</style>

<template>
  <div>
    <form @submit="addTodo">
      <input
        type="text"
        name="title"
        v-model="title"
        placeholder="Create a new Todo" />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script type="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component({
  data () {
    return {
      title: ''
    }
  },
  methods: {
    addTodo (e) {
      e.preventDefault()
      // Send up the chain via events
      this.$emit('add-todo', this.title)
      this.title = ''
    }
  }
})
export default class AddTodo extends Vue {}
</script>

<style scoped>
  form {
    display: flex;
  }
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  input[type="submit"] {
    flex: 2;
  }
</style>

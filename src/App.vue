<template>
  <div>
    <todos v-model="todos"/>
    <button @click="addTodo">Ajouter une tâche</button>
  </div>
</template>

<script>
import Todos from './components/Todos'

export default {
  components: {
    Todos
  },
  data: function () {
    return {
      todos: [{
        name: 'Demo',
        completed: true
      }]
    }
  },
  methods: {
    addTodo: function () {
      this.todos.push({
        name: 'Jean',
        completed: false
      })
    }
  }
}
</script>

<style scoped>
  button {
    font-family: "Helvetica Neue", Arial, Helvetica, sans-serif;
    background-color: #777777;
    border: 2px solid grey;
    border-radius: 4px;
    padding: 14px 40px;
  }
</style>

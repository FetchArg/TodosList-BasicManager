<template>
    <section class="todoapp">
        <header class="header">
            <h1>Todos</h1>
            <input type="text" class="new-todo" placeholder="Ajouter une tâche" v-model="newTodo" @keyup.enter="addTodo">
        </header>
        <div class="main">
            <input type="checkbox" class="toggle-all" v-model="allDone">
            <ul class="todo-list">
                <li class="todo" v-for="todo in filteredTodos" :key="todo" :class="{completed: todo.completed}">
                    <div class="view">
                        <input type="checkbox" v-model="todo.completed" class="toggle">
                        <label>{{ todo.name }}</label>
                    </div>
                </li>
            </ul>
        </div>
        <footer class="footer">
            <span class="todo-count"><strong>{{ remaining }}</strong>Tâches à faire</span>
            <ul class="filters">
                <li><a href="#" :class="{selected: filter === 'all'}" @click.prevent="filter = 'all'">Toutes</a></li>
                <li><a href="#" :class="{selected: filter === 'todo'}" @click.prevent="filter = 'todo'">A faire</a></li>
                <li><a href="#" :class="{selected: filter === 'done'}" @click.prevent="filter = 'done'">Faites</a></li>
            </ul>
        </footer>
    </section>
</template>

<script>
export default {
  data: function () {
    return {
      todos: [{
        name: 'Tache de test',
        completed: false
      }],
      newTodo: '',
      filter: 'all'
    }
  },
  computed: {
    allDone: {
      get: function () {
        return this.remaining === 0
      },
      set: function (value) {
        this.todos.forEach(todo => {
          todo.completed = value
        })
      }
    },
    remaining: function () {
      return this.todos.filter(todo => !todo.completed).length
    },
    filteredTodos: function () {
      if (this.filter === 'todo') {
        return this.todos.filter(todo => !todo.completed)
      } else if (this.filter === 'done') {
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos
    }
  },
  methods: {
    addTodo: function () {
      this.todos.push({
        completed: false,
        name: this.newTodo
      })
      this.newTodo = ''
    }
  }
}
</script>

<style src="./todos.css">

</style>

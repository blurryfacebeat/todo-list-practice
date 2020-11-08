<template>
  <div id="app">
    <h1>ToDoList Application</h1>
    <hr>

    <router-view />
    <!-- <AddTodo
      @add-todo="addTodo"
    /> -->
    <!-- Передаем массив todos в todo list -->
    <!-- <TodoList 
      :todos="todos"
      @remove-todo="removeTodo"
    /> -->
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo';

export default {
  name: 'app',
  data() {
    return {
      todos: []
    }
  },
  // Когда html запрос готов, и размещен в DOM-дереве
  mounted() {
      fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
          .then(response => response.json())
          .then(json => {
              this.todos = json
          });
  },
  methods: {
    removeTodo(id) {
      // Фильтруем массив, и оставляем элементы, где id элемента не равны удаляемому
      this.todos = this.todos.filter(t => t.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    }
  },
  components: {
    TodoList,
    AddTodo
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>

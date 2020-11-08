<template>
  <div>
    <h2>ToDoList Application</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo
      @add-todo="addTodo"
    />
    <select v-model="filter">
        <option value="all">Все задачи</option>
        <option value="completed">Выполненные</option>
        <option value="not-completed">Не выполненные</option>
    </select>
    <hr>
    <Loader v-if="loading" />
    <!-- Передаем массив todos в todo list -->
    <TodoList
        v-else-if="filteredTodos.length"
      :todos="filteredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo';
import Loader from '@/components/Loader';

export default {
  name: 'app',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  // Когда html запрос готов, и размещен в DOM-дереве
  mounted() {
      fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
          .then(response => response.json())
          .then(json => {
              this.todos = json;
              this.loading = false;
          });
  },
//   watch: {
//       filter(val) {
//           console.log(val); // будут выводиться option из select
//       }
//   },
  computed: {
      filteredTodos() {
        if (this.filter === 'all') {
            return this.todos;
        }

        if (this.filter === 'completed') {
            return this.todos.filter(a => a.completed);
        }

        if (this.filter === 'not-completed') {
            return this.todos.filter(a => !a.completed);
        }
      }
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
    AddTodo,
    Loader
  }
}
</script>
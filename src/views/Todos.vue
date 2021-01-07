<template>
  <div v-if="!loading">
    <router-link to="/">Home</router-link>
    <AddTodo @add-todo="addTodo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <TodoList
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
      v-if="filteredTodos.length"
    />
    <p v-else>No todos</p>
  </div>
  <Loader v-else />
</template>

<script>
import TodoList from "../components/TodoList";
import AddTodo from "../components/AddTodo";
import Loader from "../components/Loader";
export default {
  name: "App",
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then((response) => response.json())
      .then((json) => {
        setTimeout(() => {
          this.todos = json;
          this.loading = false;
        }, 1500);
      });
  },
  // watch: {
  //   filter(value) {
  //     let res;
  //     switch (value) {
  //       case "all":
  //         res = this.todos;
  //         break;
  //       case "completed":
  //         res = this.todos.filter((t) => t.completed);
  //         break;
  //       case "not-completed":
  //         res = this.todos.filter((t) => !t.completed);
  //         break;
  //       default:
  //         res = this.todos;
  //         break;
  //     }
  //     this.todos = res;
  //   },
  // },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      } else if (this.filter === "completed") {
        return this.todos.filter((t) => t.completed);
      } else if (this.filter === "not-completed") {
        return this.todos.filter((t) => !t.completed);
      }
    },
  },
  data() {
    return {
      todos: [],
      loading: true,
      filter: "all",
    };
  },
  components: {
    TodoList,
    AddTodo,
    Loader,
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter((t) => t.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

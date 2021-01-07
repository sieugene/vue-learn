<template>
  <div>
    <ul>
      <TodoItem
        v-for="(todo, i) of todos"
        v-bind:todo="todo"
        v-bind:index="i"
        v-bind:key="todo.id"
        v-on:remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>
<script>
import TodoItem from "./TodoItem";
export default {
  props: ["todos"],
  components: {
    TodoItem,
  },
  methods: {
    removeTodo(id) {
      this.$emit("remove-todo", id);
    },
  },
};
</script>
<style scoped>
li {
  list-style-type: none;
}
ul {
  margin: 0;
  padding: 0;
}
</style>

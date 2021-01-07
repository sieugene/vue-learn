<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" />
    <button type="submit">create</button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      title: "",
    };
  },
  methods: {
    onSubmit(e) {
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now().toString(),
          title: this.title,
          completed: false,
        };
        this.$emit("add-todo", newTodo);
        this.title = "";
      }
    },
  },
};
</script>
<style scoped>
form {
  display: flex;
  justify-content: center;
  margin-bottom: 10px;
}
input {
  width: 400px;
}
</style>

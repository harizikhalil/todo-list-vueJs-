<template>
  <div class="todo-container">
    <div v-if="todos.length > 0">
      <div :key="todo.id" v-for="todo in todos">
        <TodoItem
          :todo="todo"
          @delete-todo="$emit('delete-todo', todo.id)"
          @toggle-todo="$emit('toggle-todo', todo.id)"
          @update-todo="updateTodo"
        />
      </div>
    </div>
    <div v-else>
      <h2>add new todo</h2>
    </div>
  </div>
</template>
<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "TodoList",
  props: {
    todos: Array,
  },
  components: {
    TodoItem,
  },
  methods: {
    updateTodo(newtext, id) {
      this.$emit("update-todo", newtext, id);
    },
  },
};
</script>
<style scoped>
h2 {
  text-align: center;
  background-color: ivory;
  padding: 1em;
}
.todo-container {
  max-width: 800px;
  margin: 0 auto;
}
</style>

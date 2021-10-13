<template>
  <div class="item-card" :style="todo.done ? 'background-color:#45B8AC; ' : ''">
    <div v-if="!this.edit" class="card-content">
      <p
        class="item-text"
        :style="todo.done ? 'text-decoration:line-through' : ''"
      >
        {{ todo.text }}
      </p>
      <div class="item-option">
        <i class="fas fa-times" @click="$emit('delete-todo', todo.id)"></i>
        <i class="far fa-edit" @click="editTodo()"></i>
        <i class="fas fa-check" @click="$emit('toggle-todo', todo.id)"></i>
      </div>
    </div>
    <div v-else>
      <form @submit.prevent="updateTodo">
        <input type="text" v-model="newText" name="text" class="text-input" />
        <button type="submit" class="btn">Update todo</button>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  name: "TodoItem",
  props: {
    todo: Object,
  },
  data() {
    return {
      edit: false,
      newText: this.todo.text,
      id: this.todo.id,
    };
  },
  methods: {
    editTodo() {
      this.edit = !this.edit;
    },
    updateTodo() {
      this.$emit("update-todo", this.newText, this.todo.id);
      this.edit = !this.edit;
    },
  },
};
</script>
<style scoped>
.item-card {
  background-color: rgb(197, 191, 191);
  border-radius: 5px;
  max-width: 600px;
  padding: 1.5em;
  margin-bottom: 8px;
}
.card-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.fas,
.far {
  padding: 0.5em;
  color: #fff;
  display: block;
  cursor: pointer;
  margin-bottom: 10px;
  text-align: center;
}
.fa-times {
  background-color: rgb(194, 67, 67);
}
.fa-edit {
  background-color: rgb(185, 185, 142);
}
.fa-check {
  background-color: rgb(14, 51, 14);
}
</style>

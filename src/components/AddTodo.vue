<template>
  <form @submit.prevent="onSubmit">
    <input
      type="text"
      v-model="text"
      name="text"
      placeholder="Add Task"
      class="text-input"
    />
    <button type="submit" class="btn" :disabled="!text">Add Todo</button>
  </form>
</template>
<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: "",
    };
  },
  methods: {
    onSubmit() {
      const newTask = {
        id: Math.random(),
        text: this.text,
        done: false,
      };
      this.$emit("add-todo", newTask);
      this.text = "";
    },
  },
};
</script>
<style>
.text-input {
  background-color: #f7f7f7;
  border: 1px solid #eee;
  margin-bottom: 15px;
  width: 60%;
  height: 46px;
  padding: 10px;
}
.text-input:focus {
  outline: none;
}
.btn {
  height: 46px;
  padding: 10px;
  width: 40%;
  background-color: #2196f3;
  color: #fff;
  border-color: transparent;
  cursor: pointer;
}
.btn:disabled {
  opacity: 0.4;
  cursor: no-drop;
}
.btn:focus {
  outline: none;
}
</style>

<template>
  <!-- Co the dung map hoac for -->
  <!-- Tuy nhien trong html co 1 ham cho the p, nen ta co the dung cu phap sau -->
  <TodoItem
    v-for="todo in todos"
    :key="todo"
    :todoProps="todo"
    @item-completed="markCompleted"
    @delete-item="deleteItem"
  />
  <!-- <TodoItem/> -->
  <!-- <h1>hello world</h1> -->
</template>
<script>
import { ref } from "vue";
import TodoItem from "./TodoItem.vue";

export default {
  name: "Todos",
  components: { TodoItem },
  setup() {
    const markCompleted = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) {
          console.log("id: ", id);

          todo.completed = !todo.completed;
        }
        return todo;
      });
    };

    const deleteItem = (id) => {
      todos.value = todos.value.filter(todo => todo.id != id);
    };

    const todos = ref([
      {
        id: 1,
        title: "viec 1",
        completed: false,
      },
      {
        id: 2,
        title: "viec 2",
        completed: true,
      },
      {
        id: 3,
        title: "viec 3",
        completed: false,
      },
    ]);

    return { todos, markCompleted,deleteItem };
  },
};
</script>
<style lang=""></style>

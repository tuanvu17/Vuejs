<template>

  <AddTodo @add-todo="addTodo" />
  <!-- Co the dung map hoac for -->
  <!-- Tuy nhien trong html co 1 ham cho the p, nen ta co the dung cu phap sau -->
  <TodoItem v-for="todo in todos" :key="todo" :todoProps="todo" @item-completed="markCompleted"
    @delete-item="deleteItem" />
  <!-- <TodoItem/> -->
  <!-- <h1>hello world</h1> -->
</template>
<script>
import { ref } from "vue";
// import {v4 as uuidv4} from 'uuid';

import TodoItem from "./TodoItem.vue";
import AddTodo from "./AddTodo.vue";
import axios from "axios";
export default {
  name: "Todos",
  components: { TodoItem, AddTodo },
  setup() {
    const markCompleted = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) {
          todo.completed = !todo.completed;
        }
        return todo;
      });
    };

    const deleteItem = async id => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);

        todos.value = todos.value.filter(todo => todo.id != id);
      } catch (error) {
        console.log(error.message);

      }
    };
    const addTodo = async newTodo => {
      try {
        const res = await axios.post('https://jsonplaceholder.typicode.com/todos', newTodo);
        console.log("newTodo: ", res);
        todos.value.push(res.data)
      } catch (error) {
        console.log(error.message);

      }
    };
    const todos = ref([

    ]);

    const getAllTodos = async () => {
      try {
        const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5');
        todos.value = res.data;
        console.log(todos.value)
      } catch (error) {
        console.log(error.message);
      }
    }

    getAllTodos();

    return { todos, markCompleted, deleteItem, addTodo };
  },
};
</script>
<style lang=""></style>

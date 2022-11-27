<template>
  <div :class="['todo-item']" id="my-id">
    <input
        type="checkbox"
        :checked="todoProps.completed"
        @change="markItemCompleted"
      
    />
    <p :class="todoProps.completed ? 'is-completed' : ''">
      {{ todoProps.title }}
    </p>
    <button class="del-btn" @click="deleteItem">Delete</button>
  </div>
</template>
<script>
// import { ref } from "vue";

export default {
  name: "TodoItem",
  props: ["todoProps"],
  setup(props, context) {
    const deleteItem = () =>{
        context.emit("delete-item", props.todoProps.id)
    }
    const markItemCompleted = () => {
      context.emit("item-completed", props.todoProps.id);
    };
    return {
      markItemCompleted,deleteItem
    };
  },
};
</script>
<style>
.todo-item {
  padding: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.todo-item p {
  width: 100%;
}
.is-completed {
  text-decoration: line-through;
}
.del-btn {
  background: #f33f3f;
  color: #fff;
  border: none;
  cursor: pointer;
  width: 100px;
  height: 30px;
  text-align: center;
  border-radius: 5px;
  transition: .3s;
}
.del-btn:hover{
  background: #ff0000;
}
</style>

<template lang="">
   <form @submit="addItem" >
      <input 
      type="text" 
      placeholder="Viec moi...." 
      v-model="title"
      @input="check"
      >
      <input type="submit" value="Them" class="add-btn">
   </form>
</template>


<script>
import { ref } from "vue";
import {v4 as uuidv4} from 'uuid';

export default {
   name: 'AddTodo', 
   setup(props,context) {
      const title = ref('');
      
      const addItem = (event) => {
         event.preventDefault();

         const newItem = {
            id: uuidv4(),
            title: title.value,
            completed: false
         }
         context.emit('add-todo',newItem);
         title.value = '';
      }
      return { title ,addItem}
   }

}
</script>
<style scoped>
form {
   display: flex;
}

input[type="text"] {
   /* so cot bang 10 */
   flex: 10;
   padding: 5px;
}

input[type="submit"] {
   /* so cot bang 2 */
   flex: 2;
}
</style>
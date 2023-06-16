<template>
    <div>
      <h2>Todo List</h2>
      <form @submit.prevent="addTodo">
        <input type="text" v-model="newTodo" placeholder="Enter a new todo" />
        <button type="submit">Add Todo</button>
      </form>
  
      <ul v-for="(ele, index) in todo" :key="index">
        <input type="checkbox" v-model="ele.completed" />
        <span :class="{completed:ele.completed}">
          {{ ele }}
        </span>
          <button @click="removeTodo(index)">Remove</button>
          <button @click="editTodo(index)">Edit</button>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref,unref } from 'vue';
  
      const todo = ref([]);
      const newTodo = ref('');
      const isEditing = ref(false)
      const editingIndex = ref(null) 
  
      const addTodo = () => {
        let trimed = newTodo.value.trim();
      if(!trimed){
        newTodo.value =unref("")
        return
      }else if( isEditing.value){
        todo.value[editingIndex.value] = newTodo.value
        isEditing.value = unref(false)
      }else{
         todo.value.push(newTodo.value)
      }
     newTodo.value = unref("")
      };
  
      const removeTodo = (index) => {
        todo.value.splice(index, 1);
      };

      const editTodo = (index) => {
        let edit = todo.value[index];
      editingIndex.value = unref(index);
      isEditing.value = unref(true)
      newTodo.value = edit

      }
  
  </script>


<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
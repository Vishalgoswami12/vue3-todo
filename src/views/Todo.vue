<template>
    <div class="center">
      <h2>Todo List</h2>
      <form @submit.prevent="addTodo">
        <input class="text" type="text" v-model="newTodo" placeholder="Enter a new todo" />
        <button class="add" type="submit">Add Todo</button>
      </form>
  
      <ul v-for="(ele, index) in todo" :key="index">
        <div class="box">
        <input type="checkbox" v-model="ele.status" />
        <span :class="{completed:ele.status}">
          {{ ele.item }}
        </span>
          <button class="add" @click="removeTodo(index)">Remove</button>
          <button class="add" @click="editTodo(index)">Edit</button>
        </div>
      </ul>

      <!-- <TodoList v-for="(ele,index) in todo" :key="index" :todoName="ele.item" :index="index" :removeTodo="removeTodo" :editTodo="editTodo" /> -->

    </div>
  </template>
  
  <script setup>
  import { ref,unref } from 'vue';
  
      const todo = ref([]);
      const newTodo = ref('');
      const isEditing = ref(false);
      const editingIndex = ref(null); 
  
      const addTodo = () => {
        let trimed = unref(newTodo).trim();
      if(!trimed){
        newTodo.value =("")
        return
      }else if( isEditing.value){
        let editing = unref(todo[editingIndex].item)
        editing= newTodo.value
        isEditing.value = false
      }else{
        todo.value = [...todo.value,{item:newTodo.value,status:false}]
      }
     newTodo.value =("")
      };
  
      const removeTodo = (index) => {
        let todoSplice =unref(todo)
        todoSplice.splice(index, 1);
      };

      const editTodo = (index) => {
        let edit = todo.value[index];
      editingIndex.value = unref(index);
      isEditing.value = unref(true)
      newTodo.value = edit.item

      }
  
  </script>


<style scoped>
.completed {
  text-decoration: line-through;
}
h2{
    color: white;
    margin-top: 10px;
}
span{
    color: white;
    font-size: 20px;
}
.box{
    width: auto;
    background-color:salmon;
    margin-top: 15px;
    padding: 8px;
}
.box:hover{
    border: 1px blue solid;
}
.text{
    text-decoration: none;
    border: 1px blue solid;
    padding: 8px;
}
.text:hover{
    cursor: pointer;
}
.add{
    margin-left: 10px;
    padding: 8px;
    cursor: pointer;
}
</style>
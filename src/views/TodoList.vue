<script setup>

import { defineProps } from 'vue';
defineProps({
    todoName:{
        type:String,
        required:true,
    },
    removeTodo:{
        type:Function,
        required:true,
    }
})



</script>


<template>

<h2>{{ todoName }}</h2>
// <button>Delete</button>
// <button>Edit</button>

</template>

<style>


</style>
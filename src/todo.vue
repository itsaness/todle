<script setup>
import { ref } from 'vue';
let message = ref('');
let storages = ref([]);
let isCompleted = ref(false);
let showInput = ref(false);
let addList = ()=>{
  if(message.value.trim()!=''){
    storages.value.push({text:message.value,isCompleted:false});
  }
  
}
let complete = (index)=>{
    storages.value[index].isCompleted=!storages.value[index].isCompleted;
}
let deleteList = (index)=>{
  storages.value.splice(index,1);
  
}
let edit = (index)=>{
  const editTodo = prompt("Edit this task !");
  if(editTodo.trim()!=''&&editTodo!=null){
    storages.value[index].text=editTodo;
  }
}
</script>
<template>
    
    <div class="container">
        <h1><span class="first">T</span><span class="second">o</span><span class="third">d</span><span class="last">o</span></h1>
    <div>
    <input  type="text" placeholder=" Add your task here..." v-model="message" @keyup.enter="addList">
    <button  @click="addList" >add</button>
  </div>
  </div>
  <div class="list-container">
     <li v-for="(storage,index) in storages" :key="index" > <span :class="{'completed':storage.isCompleted,}">{{ storage.text }}</span> <button class="complete-button" @click="complete(index)">{{ storage.isCompleted ? 'Undo' : 'Complete' }}</button> <button class="edit-button" @click="edit(index)">Edit</button> <button class="delete-button" @click="deleteList(index)">delete</button></li>
  </div>
</template>
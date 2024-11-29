<template>
    <div>
      <form @submit.prevent="addTask">
        <input v-model="newTask" placeholder="할일" />
        <button type="submit">Add</button>
      </form>
  
      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          <div v-if="!task.isEditing">
            <span>{{ task.text }}</span>
            <button @click="editTask(index)">Edit</button>
            <button @click="deleteTask(index)">Delete</button>
          </div>
          <div v-else>
            <input v-model="task.text" />
            <button @click="saveTask(index)">Save</button>
          </div>
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  

  const newTask = ref('');
  const tasks = ref([]);
  

  const addTask = () => {
    if (newTask.value.trim() === '') return;
    tasks.value.push({ text: newTask.value, isEditing: false });
    newTask.value = '';
  };
  
  const editTask = (index) => {
    tasks.value[index].isEditing = true;
  };
  
  const saveTask = (index) => {
    tasks.value[index].isEditing = false;
  };
  
  const deleteTask = (index) => {
    tasks.value.splice(index, 1);
  };
  </script>
  
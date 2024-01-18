<!-- components/TaskList.vue -->
<template>
    <div class="m-auto divide-y">
      <div v-for="task in tasks" :key="task.id" class="flex justify-between py-4">

        <div class="grid gap-4 sm:gap-2">
          <div class="font-semibold text-6xl sm:text-4xl md:text-2xl lg:text-xl text-gray-800 dark:text-gray-100">{{ task.title }}</div>
          <p class="text-gray-400 dark:text-gray-200 font-semibold text-5xl sm:text-3xl md:text-xl lg:text-base">
        {{ task.description }}
        </p>
        </div>
        <div class="grid gap-2 sm:flex space-x-4">
        <button @click="editTask(task)" class="bg-blue-400 text-white text-6xl sm:text-4xl md:text-2xl lg:text-xl px-5 sm:h-11 h-16 rounded">Edit</button>
        <button @click="deleteTask(task.id)" class="bg-red-600 text-white text-6xl sm:text-4xl md:text-2xl lg:text-xl px-5 sm:h-11 h-16 rounded">Delete</button>
      </div>
      </div>
    </div>
  </template>
  
  <script>
import { ref } from 'vue';

export default {
  props: {
    tasks: {
      type: Array,
      default: [],
    },
  },
  setup(props, { emit }) {
    const editTask = (task) => {
      emit('editTask', task);
    };

    const deleteTask = (id) => {
      emit('confirmDelete', id);
    };

    return {
      editTask,
      deleteTask,
    };
  },
};
</script>
  
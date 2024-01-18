<!-- components/AddEditTaskForm.vue -->
<template>
    <div>
      <h2 class="text-2xl font-bold mb-4">{{ isEditing ? 'Edit Task' : 'Add Task' }}</h2>
  
      <form @submit.prevent="submitForm">
        <div class="mb-4">
          <label for="title" class="block text-sm font-semibold text-gray-600">Title:</label>
          <input v-model="form.title" type="text" id="title" class="border p-2 w-full" required />
        </div>
  
        <div class="mb-4">
          <label for="description" class="block text-sm font-semibold text-gray-600">Description:</label>
          <textarea v-model="form.description" id="description" class="border p-2 w-full" rows="4"></textarea>
        </div>
  
        <div>
          <button type="submit" class="bg-blue-500 text-white p-2">{{ isEditing ? 'Update Task' : 'Add Task' }}</button>
        </div>
      </form>
    </div>
  </template>
  
  <script>
  import { ref, watch } from 'vue';
  
  export default {
    props: {
      isEditing: Boolean,
      taskToEdit: Object,
      addTask: Function,
      updateTask: Function,
    },
    setup(props) {
      const form = ref({
        title: '',
        description: '',
      });
  
      watch(() => props.taskToEdit, () => {
        if (props.isEditing) {
          form.value.title = props.taskToEdit.title;
          form.value.description = props.taskToEdit.description;
        } else {
          form.value.title = '';
          form.value.description = '';
        }
      });
  
      const submitForm = () => {
        if (props.isEditing) {
          props.updateTask(form.value);
        } else {
          props.addTask(form.value);
        }
  
        form.value.title = '';
        form.value.description = '';
      };
  
      return {
        form,
        submitForm,
      };
    },
  };
  </script>
  
  <style scoped>
  /* Add any custom styles here */
  </style>
  
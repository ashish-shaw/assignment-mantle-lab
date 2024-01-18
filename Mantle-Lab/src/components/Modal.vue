<template>
    <div v-if="isOpen" class="popup-overlay fixed top-0 left-0 w-full h-full bg-gray-800 flex justify-center items-center">
      <div class="bg-white rounded-lg p-4 shadow-xl w-[80%] h-[40%] md:h-auto md:max-w-96">
        <div class="flex border-b justify-between pb-4">
            <h2 class="text-6xl sm:text-5xl md:text-3xl lg:text-2xl font-semibold text-gray-800">{{ taskToEdit ? "Edit Task" : "Add Task"}}</h2>
          <button @click="closePopup" class="bg-none border-none cursor-pointer text-5xl sm:text-3xl md:text-2xl lg:text-xl text-gray-500">&times;</button>
        </div>
        <div>
            <form @submit.prevent="submitForm">
        <div class="my-4">
          <label for="title" class="block text-3xl sm:text-2xl md:text-xl lg:text-base font-semibold text-gray-800">Title:</label>
          <input v-model="form.title" type="text" id="title" class="border sm:p-2 p-4 w-full text-3xl sm:text-2xl md:text-xl lg:text-base" required />
        </div>
  
        <div class="mb-4">
          <label for="description" class="block text-3xl sm:text-2xl md:text-xl lg:text-base font-semibold text-gray-800">Description:</label>
          <textarea v-model="form.description" id="description" class="border sm:p-2 p-4 w-full text-3xl sm:text-2xl md:text-xl lg:text-base" rows="4"></textarea>
        </div>
  
        <div class="flex justify-end">
          <button type="submit" class="bg-green-600 text-6xl sm:text-4xl md:text-2xl lg:text-xl h-24 sm:h-11 text-white sm:py-2 py-4 px-5 rounded">{{ taskToEdit ? "Update" : "Add"}}</button>
        </div>
      </form>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, watchEffect } from 'vue';
  
  export default {
    props: {
      isOpen: {
        type: Boolean,
        required: false,
      },
      taskToEdit: {
        type: Object,
        required: false,
      },
    },
    setup(props, { emit }) {
      const form = ref({
        id: 0,
        title: '',
        description: '',
      });
  
      if (props.taskToEdit) {
        watchEffect(() => {
          form.value = { ...props.taskToEdit };
        });
      }
  
      const closePopup = () => {
        emit('close');
      };
  
      const submitForm = () => {
        if (props.taskToEdit) {
          emit('updateTask', form.value);
        } else {
          emit('addTask', form.value);
        }
        closePopup();
      };
  
      return {
        form,
        closePopup,
        submitForm,
      };
    },
  };
  </script>
  
  <style scoped>
  .popup-overlay {
    background: rgba(0, 0, 0, 0.5);
  }
  </style>
  
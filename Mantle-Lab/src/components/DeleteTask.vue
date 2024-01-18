<template>
    <div v-if="isOpen" class="popup-overlay fixed top-0 left-0 w-full h-full bg-gray-800 flex justify-center items-center">
      <div class="bg-white rounded-lg p-4 shadow-xl w-[80%] h-[40%] md:h-auto md:max-w-96">
        <div class="flex border-b justify-between pb-4">
            <h2 class="text-6xl sm:text-5xl md:text-3xl lg:text-2xl font-semibold text-red-500">Delete</h2>
          <button @click="closePopup" class="bg-none border-none cursor-pointer text-5xl sm:text-3xl md:text-2xl lg:text-xl text-gray-500">&times;</button>
        </div>
        <div class="py-2">
            Are you sure you want to delete this task?
        </div>
        <div class="flex justify-end pt-2">
        <button @click="confirmDelete" class="bg-red-600 text-6xl sm:text-4xl md:text-2xl lg:text-xl h-20 sm:h-11 text-white sm:py-2 py-3 px-5 rounded">Delete</button>
      </div>
      </div>
    </div>
  </template>
  
  <script>
import { ref } from 'vue';

export default {
  props: {
    isOpen: {
      type: Boolean,
      required: false,
    },
    deleteTaskId: {
      type: Number,
      required: false,
    },
  },
  setup(props, { emit }) {
    const closePopup = () => {
      emit("closeDelete");
    };

    const confirmDelete = () => {
      emit("deleteTask", props.deleteTaskId);
      closePopup();
    };

    return {
      closePopup,
      confirmDelete,
    };
  },
};
</script>

  
  <style scoped>
  .popup-overlay {
    background: rgba(0, 0, 0, 0.5);
  }
  </style>
  
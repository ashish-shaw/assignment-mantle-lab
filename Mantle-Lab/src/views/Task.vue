<template>
  <div class="p-6 shadow border rounded">
    <div class="flex justify-between items-center mb-4">
        <h2 class="text-8xl sm:text-6xl md:text-4xl lg:text-2xl text-bold text-gray-800 mt-2 dark:text-gray-100">Task Tracker</h2>
        <button
      @click="openPopup"
      class="bg-green-600 text-white text-6xl sm:text-4xl md:text-2xl lg:text-xl text-bold py-2 px-5 rounded"
    >
       Add Task
    </button>
    </div>
    
    <TaskList :tasks="tasks" @editTask="editTask" @confirmDelete="confirmDelete" />
    
    
    <Modal v-if="isPopupOpen" :isOpen="isPopupOpen" :taskToEdit="taskToEdit" @addTask="addTask" @updateTask="updateTask" @close="closePopup"/>
    <DeleteTask v-if="isDelete" :isOpen="isDelete" :deleteTaskId="deleteTaskId"  @deleteTask="deleteTask" @closeDelete="closePopup"/>
  </div>
</template>

<script>
import { ref } from 'vue';
import TaskList from '@/components/TaskList.vue';
import Modal from '@/components/Modal.vue';
import DeleteTask from '../components/DeleteTask.vue';

export default {
  name: 'Task',
  components: {
    TaskList,
    Modal,
    DeleteTask
  },
  setup() {
    const tasks = ref([
      { id: 1, title: 'Task 1', description: 'Description 1' },
      { id: 2, title: 'Task 2', description: 'Description 2' },
    ]);

    const taskToEdit = ref(null);
    const isPopupOpen = ref(false);
    const isDelete = ref(false);
    const deleteTaskId = ref(null);

    const openPopup = () => {
      isPopupOpen.value = true;
      taskToEdit.value = null;
    };

    const closePopup = () => {
      isPopupOpen.value = false;
      isDelete.value = false
    };

    const addTask = (newTask) => {
      tasks.value.push({ id: Date.now(), ...newTask });
      console.log(tasks.value);
    };

    const editTask = (task) => {
      isPopupOpen.value = true;
      taskToEdit.value = task;
    };

    const updateTask = (updatedTask) => {
      const index = tasks.value.findIndex((task) => task.id === updatedTask.id);
      if (index !== -1) {
        tasks.value.splice(index, 1, updatedTask);
      }
    };

    const confirmDelete = (taskId) => {
        isDelete.value = true;
        deleteTaskId.value = taskId;
    }

    const deleteTask = (deleteID) => {
        tasks.value = tasks.value.filter((task) => task.id !== deleteID);
    };

    return {
      tasks,
      taskToEdit,
      isPopupOpen,
      isDelete,
      openPopup,
      closePopup,
      addTask,
      editTask,
      updateTask,
      deleteTask,
      confirmDelete,
      deleteTaskId
    };
  },
};
</script>

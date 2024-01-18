<!-- DarkModeToggle.vue -->
<template>
    <div @click="toggleDarkMode" class="cursor-pointer text-2xl text-[#333]">
      <span v-if="isDarkMode">&#127769;</span>
      <span v-else>☀️</span>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    setup() {
      const isDarkMode = ref(false);
  
      const toggleDarkMode = () => {
        isDarkMode.value = !isDarkMode.value;
        document.body.classList.toggle('dark', isDarkMode.value);
      };
  
      return {
        isDarkMode,
        toggleDarkMode,
      };
    },
  };
  </script>
  
  
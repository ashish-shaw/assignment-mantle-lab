<template>
  <div>
  <div id="app" class="dark:bg-black dark:text-white">
    <Task/>    
    <DarkMode class="fixed top-0 right-0" @dark-mode-toggled="updateDarkModeStatus" />
</div>

</div>
</template>

<script>
import { ref } from 'vue';
import Task from "./views/Task.vue";
import DarkMode from "./components/DarkMode.vue";

export default {
  components: {
    Task,
    DarkMode
  },
  setup() {
    const isDarkMode = ref(false);

    const updateDarkModeStatus = (isDarkMode) => {
      isDarkMode.value = isDarkMode;
    };

    return {
      isDarkMode,
      updateDarkModeStatus,
    };
  },
};
</script>

<style>
body{
  @apply bg-white dark:bg-black
}
</style>

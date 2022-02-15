<script setup>
import Todos from './components/Todos.vue'
</script>

<template>
  <div>
    <div class="text-center">
      <h4 class="display-6 text-uppercase m-0">To Do APP</h4>
      <small class="text-muted text-center">Add or Remove Your Daily Task</small>
    </div>
    <Todos />
  </div>
</template>

<style>
#app {
  font-family: poppins, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 2rem;
}
</style>

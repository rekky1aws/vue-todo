<script setup lang="ts">
import Task from '@/features/todo/components/Task.vue';

const props = defineProps({
  tasks: Array
});

console.log(props.tasks);
</script>
<!--  -->
<template>
  <ul>
    <Task v-for="task in props.tasks" :task="task"></Task>        
  </ul>
</template>
<!--  -->
<style scoped>
</style>
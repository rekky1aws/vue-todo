<script setup lang="ts">
import Task from '@/features/todo/components/Task.vue';

const props = defineProps({
  tasks: Array
});

const tasks = ref([
    {
        title: "Test completed",
        completed: true,
        date: Date.now()
    },
    {
        title: "Test not completed",
        completed: false,
        date: Date.now()
    }
]);

const sortTasks = () => {
    tasks.value = tasks.value.sort((a,b) => {
        return a.title.toLowerCase() < b.title.toLowerCase() ? -1 : 1;
    });

    tasks.value = tasks.value.sort((a,b) => {
        return a.completed < b.completed ? -1 : 1;
    });
};

const addTask = (newTaskName:string) => {
    if (!newTaskName.length) {
        throw new Error("No empty task name");
    }

    tasks.value.push({
        title:newTaskName,
        completed: false,
        date: Date.now()
    });

    newTask.value = "";
    sortTasks();
};

const deleteTask = (task:any) => {
    if (!window.confirm(`Êtes-vous sur de de vouloir supprimer la tâche "${task.title}"`)) {
        console.log("Task not deleted");
        return false;
    }

    tasks.value = tasks.value.filter((taskE) => {
        return taskE !==  task;
    });
    sortTasks();
};

const completeTask = (task:any) => {
    task.completed = !task.completed;
    sortTasks();
};

sortTasks();

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
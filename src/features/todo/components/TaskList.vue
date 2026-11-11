<script setup lang="ts">
import Task from '@/features/todo/components/Task.vue';
import {ref} from 'vue';

const emits = defineEmits([
"nbTasks"
]);

const newTask = ref('');

const tasks = ref([]);
emits("nbTasks", tasks.value.length);

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
  saveToLocalStorage();
  emits('nbTasks', tasks.value.length);
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
  saveToLocalStorage();
};

const completeTask = (task:any) => {
  task.completed = !task.completed;
  sortTasks();
  saveToLocalStorage();
};

const saveToLocalStorage = () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value));

};

const loadFromLocalStorage = () => {
  tasks.value = JSON.parse(localStorage.getItem('tasks'));
};

loadFromLocalStorage();
sortTasks();

</script>
<!--  -->
<template>
  <div>
    <form action=""  @submit.prevent="addTask(newTask)">
      <input v-model="newTask" type="text" placeholder="Nouvelle Tache">
      <button :disabled="newTask.length == 0">Ajouter la tache</button>
    </form>
  </div>
  <div>
    <ul v-if="tasks.length">
      <Task
      v-for="task in tasks"
      :task="task"
      @complete="completeTask(task)"
      @delete="deleteTask(task)"
      />
    </ul>
    <div v-else>Pas de tâches à afficher</div>
  </div>
</template>
<!--  -->
<style scoped>
</style>
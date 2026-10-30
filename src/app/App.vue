<script setup lang="ts">
import TaskList from '@/features/todo/components/TaskList.vue';
import {ref} from 'vue';

const newTask = ref ("");
</script>

<template>
    <div>
        <form action=""  @submit.prevent="addTask(newTask)">
            <input v-model="newTask" type="text" placeholder="Nouvelle Tache">
            <button :disabled="newTask.length == 0">Ajouter la tache</button>
        </form>
    </div>
    <div v-if="tasks.length">
        <TaskList :tasks="tasks"></TaskList>
    </div>
    <div v-else>Aucune tâche pour le moment</div>
</template>

<style scoped>

</style>

<script setup lang="ts">
import {ref} from 'vue';

const newTask = ref ("");
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
}

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
}

const deleteTask = (task:any) => {
    if (!window.confirm(`Êtes-vous sur de de vouloir supprimer la tâche "${task.title}"`)) {
        console.log("Task not deleted");
        return false;
    }

    tasks.value = tasks.value.filter((taskE) => {
        return taskE !==  task;
    });
    sortTasks();
}

const completeTask = (task:any) => {
    task.completed = !task.completed;
    sortTasks();
}

sortTasks();
</script>

<template>
    <div>
        <form action=""  @submit.prevent="addTask(newTask)">
            <input v-model="newTask" type="text" placeholder="Nouvelle Tache">
            <button :disabled="newTask.length == 0">Ajouter la tache</button>
        </form>
    </div>
    <div v-if="tasks.length">
        <ul>
            <li v-for="task in tasks" :class="{completed: task.completed}" :key="task.title">
                <button class="checkBtn" @click="completeTask(task)">
                    {{ task.completed ? "o" : "O" }}
                </button>
                <button class="delBtn" @click="deleteTask(task)">X</button>
                <span>{{ task.title }}</span>
            </li>
        </ul>
    </div>
    <div v-else>Aucune tâche pour le moment</div>
</template>

<style scoped>
.completed {
    opacity: 0.5;
}

.completed > span {
    text-decoration: line-through;
}

li {
    display: flex;
    gap: 0.5rem;
    margin: 0.25rem;
}

li > button {
    width: 2rem;
    font-weight: bold;
}

.checkedBtn:hover {
    color: lime;
}

.delBtn {
    color:red;
}
</style>

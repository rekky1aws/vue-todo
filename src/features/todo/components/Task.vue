<script setup lang="ts">
const props = defineProps({
  task: Object
});

const emits = defineEmits([
  "complete",
  "delete"
]);

const completeTask = (task: Object) => {
  emits('complete', task);
};

const deleteTask = (task: Object) => {
  emits('delete', task);
};
</script>
<!--  -->
<template>
  <li :class="{completed: task.completed}" :key="task.title">
    <button class="checkBtn" @click="completeTask(task)">
      {{ task.completed ? "o" : "O" }}
    </button>
    <button class="delBtn" @click="deleteTask(task)">X</button>
    <span>{{ task.title }}</span>
  </li>
</template>
<!--  -->
<style scoped>
li {
    display: flex;
    gap: 0.5rem;
    margin: 0.25rem;
}

li > button {
    width: 2rem;
    font-weight: bold;
}

.completed {
    opacity: 0.5;
}

.completed > span {
    text-decoration: line-through;
}

.checkBtn:hover {
    color: lime;
}

.delBtn {
    color:red;
}

</style>
<script setup lang="ts">
const props = defineProps({
  task: {
    type: Object,
    required: true
  }
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
  <li :class="{completed: props.task.completed}" :key="props.task.title">
    <button class="checkBtn" @click="completeTask(props.task)">
      {{ props.task.completed ? "o" : "O" }}
    </button>
    <button class="delBtn" @click="deleteTask(props.task)">X</button>
    <span>{{ props.task.title }}</span>
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
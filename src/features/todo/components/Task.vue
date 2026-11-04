<script setup lang="ts">
import DeleteButton from '@/shared/ui/DeleteButton.vue';
import PrimaryButton from '@/shared/ui/PrimaryButton.vue';

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
    <PrimaryButton class="checkBtn" @click="completeTask(props.task)">
      {{ props.task.completed ? "o" : "O" }}
    </PrimaryButton>
    <DeleteButton @click="deleteTask(props.task)">X</DeleteButton>
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

</style>
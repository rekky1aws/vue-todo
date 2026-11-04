<script setup lang="ts">
</script>

<template>
  <button class="delBtn">
    <slot>X</slot>
  </button>
</template>

<style scoped>
.delBtn {
  color:white;
  background-color:red;
  border:none;
  border-radius: 1rem;
}
</style>
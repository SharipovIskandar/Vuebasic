<template>
  <ul>
    <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @edit-task="editTask"
        @delete-task="deleteTask"
    />
  </ul>
</template>

<script setup>
import { defineProps } from 'vue';
import TaskItem from './TaskItem.vue';

const props = defineProps({
  tasks: {
    type: Array,
    required: true,
  },
  editTask: Function,
  deleteTask: Function,
});
</script>

<style scoped>
/* Stil kerak bo'lsa qo'shishingiz mumkin */
</style>

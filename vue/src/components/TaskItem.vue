<template>
  <li>
    <input type="checkbox" v-model="task.completed" @change="updateTask" />
    <span class="{ completed: task.completed }">{{ task.content }}</span>
    <button @click="editTask(task)">Tahrirlash</button>
    <button @click="deleteTask(task.id)">O'chirish</button>
  </li>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  task: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(['edit-task', 'delete-task']);

const editTask = (task) => {
  emit('edit-task', task);
};

const deleteTask = (taskId) => {
  emit('delete-task', taskId);
};

const updateTask = () => {
  emit('edit-task', props.task);
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: grey;
}
</style>

<template>
  <form @submit.prevent="submitTask">
    <input type="text" v-model="newTask.content" placeholder="Yangi vazifa qo'shish" required />
    <button type="submit">Qo'shish</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';

const newTask = ref({
  content: '',
  completed: false,
  userId: 1,
});

const emit = defineEmits(['add-task']);

const submitTask = () => {
  emit('add-task', newTask.value);
  newTask.value.content = '';
};
</script>



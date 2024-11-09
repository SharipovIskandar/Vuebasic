<template>
  <div>
    <h1>{{ title }}</h1>
    <form @submit="addNewTask">
      <input type="text" id="new-task" v-model="newTask" placeholder="Add a new task" />
      <button type="submit">Add task</button>
    </form>
    <ul>
      <li v-for="task in list" :key="task.id">
        <input type="checkbox" v-model="task.completed" />
        <span v-if="task.isEditing">
          <input type="text" v-model="task.content" @blur="saveEdit(task)" />
        </span>
        <span v-else class="{ completed: task.completed }">
          {{ task.content }}
        </span>
        <button @click="editTask(task)">Edit</button>
        <button @click="deleteTask(task.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const title = "To Do";
const newTask = ref("");
const list = ref([]);

onMounted(() => {
  const savedTasks = localStorage.getItem("tasks");
  if (savedTasks) {
    list.value = JSON.parse(savedTasks);
  }
});

const saveTasksToLocalStorage = () => {
  localStorage.setItem("tasks", JSON.stringify(list.value));
};

const addNewTask = (e) => {
  e.preventDefault();
  if (newTask.value.trim() !== "") {
    const id = list.value.length ? list.value[list.value.length - 1].id + 1 : 1;
    const task = { id: id, content: newTask.value, completed: false, isEditing: false };
    list.value.push(task);
    newTask.value = "";
    saveTasksToLocalStorage();
  }
};

const deleteTask = (taskId) => {
  list.value = list.value.filter((task) => task.id !== taskId);
  saveTasksToLocalStorage();
};

const editTask = (task) => {
  task.isEditing = true;
};

const saveEdit = (task) => {
  task.isEditing = false;
  saveTasksToLocalStorage();
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: grey;
}
</style>

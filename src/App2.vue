<script setup lang="ts">
import { onMounted, ref } from "vue";

const title = ref("Vue Jobs");
const status = ref("active");
const tasks = ref([
  { id: 1, title: "Task 1", completed: false },
  { id: 2, title: "Task 2", completed: true },
]);
const newTask = ref("");
const googleLink = "https://google.com";

function toggleStatus() {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
  console.log("Status changed to:", status.value);
}

function addTask() {
  if (newTask.value.trim() !== "") {
    tasks.value.push({
      id: tasks.value.length + 1,
      title: newTask.value,
      completed: false,
    });
    newTask.value = "";
  }
}

function deleteTask(taskId: number) {
  tasks.value = tasks.value.filter((task) => task.id !== taskId);
}

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    tasks.value = data.slice(0, 10).map((task: any) => ({
      id: task.id,
      title: task.title,
      completed: task.completed,
    }));
  } catch (error) {
    console.log("Error fetching tasks:", error);
  }
});
</script>

<template>
  <h1>{{ title }}</h1>
  <br />
  <p v-if="status === 'active'">User is Active</p>
  <p v-else-if="status === 'pending'">User is Pending</p>
  <p v-else>Status is InActive</p>
  <br />

  <div>
    <h3>Tasks:</h3>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <span>
          {{ task.title }} - {{ task.completed ? "Completed" : "Pending" }}
        </span>
        <button @click="deleteTask(task.id)">Delete task</button>
      </li>
    </ul>
  </div>

  <br />
  <a :href="googleLink" target="_blank">Google</a>
  <br />
  <button @click="toggleStatus">Change Status</button>

  <br />
  <form @submit.prevent="addTask">
    <label for="newTask"></label>
    <input type="text" v-model="newTask" placeholder="Add a new task" />
    <button type="submit">Add Task</button>
  </form>
</template>

<style scoped>
h1 {
  color: red;
}
</style>

<script setup>
import { ref, onMounted } from "vue";

const name = ref("Jhon Doe");
const status = ref("active");
const tasks = ref(["Task one", "Task Two", "Task Three"]);
const link = ref("https://www.google.com");
const newTask = ref();

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};
const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask = "";
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await res.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log("Error featching tasks");
  }
});
</script>

<template>
  <h1>{{ name }}</h1>
  <!-- if else statement start -->
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pendig'">User is pending</p>
  <p v-else="status !== 'active'">User is inactive</p>
  <!-- v-bind:href="link" or :href="link" -->
  <a :href="link">Click for google</a>
  <br />
  <!-- @click and v-on:click are same -->
  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
  <button @click.prevent="toggleStatus">Change Status</button>
  <br />
  <!-- Form  -->
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>
  <br />
  <!-- if else statement end -->
  <h3>Tasks:</h3>
  <br />
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>
</template>

<style scoped>
h1 {
  color: red;
}
</style>

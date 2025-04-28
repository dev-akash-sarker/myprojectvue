<script>
// options are data()
export default {
  data() {
    return {
      name: "Jhon doe",
      status: "inactive",
      tasks: ["task one", "task two", "task three"],
      link: "https://www.google.com",
    };
  },
  /**
   * methods for independent functions
   */
  methods: {
    toggleStatus() {
      if (this.status === "active") {
        this.status = "pending";
      } else if (this.status === "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    },
  },
};
</script>

<template>
  <h1>{{ this.name }}</h1>
  <!-- if else statement start -->
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pendig'">User is pending</p>
  <p v-else="status !== 'active'">User is inactive</p>
  <!-- if else statement end -->
  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <!-- v-bind:href="link" or :href="link" -->
  <a v-bind:href="link">Click for google</a>
  <br />
  <!-- @click and v-on:click are same -->
  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
  <button @click="toggleStatus">Change Status</button>
</template>

<style scoped>
h1 {
  color: red;
}
</style>

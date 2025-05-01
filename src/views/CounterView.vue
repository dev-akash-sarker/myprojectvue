<script setup>
import { ref } from "vue";
const count = ref(0);
const tasks = ref(["task one", "task two", "task three", "task four"]);
const add = () => {
  count.value++;
};

const minus = () => {
  count.value--;
};
</script>
<template>
  <div class="w-[100px] mx-auto">
    <button @click="add">+</button>
    <h1>{{ count }}</h1>
    <button @click="minus">-</button>
  </div>
</template>

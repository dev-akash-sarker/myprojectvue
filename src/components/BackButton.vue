<script setup>
import { defineProps } from "vue";
import { RouterLink } from "vue-router";

defineProps({
  tolink: String,
});
</script>
<template>
  <!-- Go Back -->
  <section>
    <div class="container m-auto py-6 px-6">
      <RouterLink
        :to="tolink"
        class="text-green-500 hover:text-green-600 flex items-center"
      >
        <i class="pi pi-arrow-circle-left"></i> Back to Job Listings
      </RouterLink>
    </div>
  </section>
</template>

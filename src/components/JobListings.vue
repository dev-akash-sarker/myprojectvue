<script setup>
import { ref, defineProps } from "vue";
import JobListing from "@/components/JobListing.vue";
import jobData from "@/jobs.json";

const jobs = ref(jobData);
defineProps({
  limits: Number,
  showButton: {
    type: Boolean,
    default: false,
  },
});
</script>
<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <div class="container-xl lg:container m-auto">
        <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
          Browse Jobs
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <JobListing
            v-for="job in jobs.slice(0, limits || jobs.length)"
            :key="job.id"
            :job="job"
          />
        </div>
      </div>
    </div>
  </section>
  <section class="m-auto max-w-lg my-10 px-6" v-if="showButton">
    <a
      href="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</a
    >
  </section>
  <div v-for="job in jobs" :key="job.id">
    {{ job.title }}
  </div>
</template>

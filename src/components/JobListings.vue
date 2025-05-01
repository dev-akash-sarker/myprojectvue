<script setup>
import { reactive, defineProps, onMounted } from "vue";
import JobListing from "@/components/JobListing.vue";
// import jobData from "@/jobs2.json";
import { RouterLink } from "vue-router";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import axios from "axios";

// const jobs = ref(jobData);
defineProps({
  limits: Number,
  showButton: {
    type: Boolean,
    default: false,
  },
});

const state = reactive({
  jobs: [],
  isLoading: true,
});

onMounted(async () => {
  try {
    const response = await axios.get("/api/jobs");
    state.jobs = response.data;
  } catch (error) {
    console.error("Error fetching jobs", error);
  } finally {
    state.isLoading = false;
  }
});
</script>
<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <div class="container-xl lg:container m-auto">
        <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
          Browse Jobs
        </h2>
        <!-- Show loading spinner while loading is true -->
        <div v-if="state.isLoading" class="text-center text-gray-500">
          <PulseLoader />
        </div>
        <!-- Show job litsing when done loading -->
        <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <JobListing
            v-for="job in state.jobs.slice(0, limits || state.jobs.length)"
            :key="job.id"
            :job="job"
          />
        </div>
      </div>
    </div>
  </section>
  <section class="m-auto max-w-lg my-10 px-6" v-if="showButton">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</RouterLink
    >
  </section>
  <div v-for="job in jobs" :key="job.id">
    {{ job.title }}
  </div>
</template>

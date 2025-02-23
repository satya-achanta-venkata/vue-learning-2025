<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h1 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h1>
      <div v-if="state.isLoading">Loading....</div>
      <div v-else class="grid grid-cols-1 gap-6 md:grid-cols-3">
        <JobListing
          v-for="job in state.jobs.slice(0, limit)"
          :key="job.id"
          class="job-listing"
          :job="job"
        />
      </div>
    </div>
  </section>
  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs
    </RouterLink>
  </section>
</template>

<script setup lang="ts">
import { ref, defineProps, onMounted, reactive } from "vue";
import { RouterLink } from "vue-router";
import axios from "axios";
import JobListing from "@/components/JobListing.vue";

interface Job {
  id: number;
  title: string;
  company: string;
  location: string;
  salary: string;
  type: string;
  experience: string;
  description: string;
  requirements: string[];
  tags: string[];
  created_at: string;
}

const state = reactive({
  isLoading: true,
  jobs: [] as Job[],
});

defineProps({
  limit: {
    type: Number,
    default: 5,
  },
  showButton: {
    type: Boolean,
    default: false,
  },
});

onMounted(async () => {
  try {
    const response = await axios.get("/api/jobs");
    state.jobs = response.data;
  } catch (error) {
    console.error("Error fetching job listings:", error);
  } finally {
    state.isLoading = false;
  }
});
</script>

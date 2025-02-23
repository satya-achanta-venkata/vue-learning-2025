<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h1 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h1>
      <div class="grid grid-cols-1 gap-6 md:grid-cols-3">
        <JobListing
          v-for="job in jobs.slice(0, limit)"
          :key="job.id"
          class="job-listing"
          :job="job"
        />
      </div>
    </div>
  </section>
  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <a
      href="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</a
    >
  </section>
</template>

<script setup lang="ts">
import { ref, defineProps } from "vue";
import JobData from "@/jobs.json";
import JobListing from "@/components/JobListing.vue";

const jobs = ref(JobData);
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
</script>

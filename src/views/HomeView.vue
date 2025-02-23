<template>
  <Hero />
  <Homecards />
  <JobListings :limit="3" :show-button="true" />
</template>

<script setup lang="ts">
import Hero from "@/components/Hero.vue";
import Homecards from "@/components/Homecard.vue";
import JobListings from "@/components/JobListings.vue";
</script>

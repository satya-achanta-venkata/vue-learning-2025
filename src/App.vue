<template>
  <Navbar />
  <Hero />
  <Homecards />
  <JobListings :limit="3" :show-button="true" />
</template>

<script setup lang="ts">
import Navbar from "@/components/Navbar.vue";
import Hero from "@/components/Hero.vue";
import Homecards from "@/components/Homecard.vue";
import JobListings from "@/components/JobListings.vue";
</script>

<style scoped></style>

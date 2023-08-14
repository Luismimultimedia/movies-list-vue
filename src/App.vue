<script setup>
// pages
import Home from "./pages/Home/Home.vue";

// data
import { items } from "./movies.json";

</script>

<template>
  <main class="lg:container mx-auto p-4">
    <Home :movies="items"/>
  </main>
</template>

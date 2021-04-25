<template>
  <header class="text-center bg-blue-500 text-gray-100 p-4 mb-10">
    <h1 class="text-3xl md:text-5xl font-bold mb-3">
      <i class="fas fa-viruses"></i> Covid-19 Tracker
    </h1>

    <p>
      API by
      <a href="https://covid19api.com" class="text-blue-300">covid19api.com</a>
    </p>
  </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Header",
});
</script>

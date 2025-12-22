<script setup>
import { ref } from "vue";

const product = ref("Socks");
const description = ref("A pair of warm, fuzzy socks");
</script>

<template>
  <div class="flex flex-col p-4">
    <div class="flex flex-wrap">
      <div class="w-1/2">
        <h1 class="text-5xl/tight mb-5">{{ product }}</h1>
        <p class="text-xl">{{ description }}</p>
      </div>
    </div>
  </div>
</template>

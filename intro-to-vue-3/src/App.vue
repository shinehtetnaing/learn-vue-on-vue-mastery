<script setup>
import { ref } from "vue";
import ProductDisplay from "./components/ProductDisplay.vue";

const cart = ref(0);

const premium = ref(true);
</script>

<template>
  <nav class="w-full h-20 bg-green-300 px-8 flex justify-end items-center">
    <div
      class="rounded-lg border-2 border-gray-950 flex items-center justify-center text-xl font-semibold text-black p-5 h-10"
    >
      Cart ({{ cart }})
    </div>
  </nav>
  <ProductDisplay :premium="premium"></ProductDisplay>
</template>

<script setup>
import { ref } from "vue";
import socksGreenImage from "./assets/images/socks_green.jpeg";

const product = ref("Socks");
const description = ref("A pair of warm, fuzzy socks");
const image = ref(socksGreenImage);
const inventory = ref(100);
</script>

<template>
  <div class="flex flex-col p-4">
    <div class="flex gap-10">
      <div class="w-1/2">
        <img :src="image" class="shadow rounded-xl" />
      </div>
      <div class="w-1/2">
        <h1 class="text-5xl/tight mb-5">{{ product }}</h1>
        <p class="text-xl mb-3">{{ description }}</p>
        <p class="text-lg font-semibold" v-if="inventory > 10">In Stock</p>
        <p
          class="text-lg font-semibold"
          v-else-if="inventory <= 10 && inventory > 0"
        >
          Almost Sold Out!
        </p>
        <p class="text-lg font-semibold" v-else>Out of Stock</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import socksGreenImage from "./assets/images/socks_green.jpeg";
import socksBlueImage from "./assets/images/socks_blue.jpeg";

const product = ref("Socks");
const description = ref("A pair of warm, fuzzy socks");
const image = ref(socksGreenImage);

const inventory = ref(100);

const varients = ref([
  { id: 1, color: "green", image: socksGreenImage },
  { id: 2, color: "blue", image: socksBlueImage },
]);

const listColor = (color) => {
  switch (color) {
    case "blue":
      return "before:text-blue-500";
    case "green":
      return "before:text-green-500";
    default:
      return "before:text-gray-400";
  }
};

const cart = ref(0);

const addToCart = () => (cart.value += 1);

const removeFromCart = () => {
  if (cart.value >= 1) {
    cart.value -= 1;
  }
};

const updateImage = (varientImage) => {
  image.value = varientImage;
};
</script>

<template>
  <nav class="w-full h-20 bg-green-300 px-8 flex justify-end items-center">
    <div
      class="rounded-lg border-2 border-gray-950 flex items-center justify-center text-xl font-semibold text-black p-5 h-10"
    >
      Cart ({{ cart }})
    </div>
  </nav>
  <div class="flex flex-col px-8 py-12">
    <div class="flex flex-col sm:flex-row gap-10">
      <div class="w-sm sm:w-125">
        <img
          :src="image"
          class="shadow rounded-xl"
          :class="{ 'opacity-50': !inventory }"
        />
      </div>
      <div>
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
        <div class="mt-6">
          <h2 class="text-xl font-semibold mb-2">Varients</h2>
          <ul class="list-none w-fit">
            <li
              v-for="varient in varients"
              :key="varient.id"
              class="before:content-['⬤'] before:mr-2 before:text-3xl flex items-center capitalize"
              :class="listColor(varient.color)"
              @mouseover="updateImage(varient.image)"
            >
              {{ varient.color }}
            </li>
          </ul>
        </div>
        <button
          class="mt-6 mr-5"
          @click="addToCart"
          :disabled="inventory <= 0"
          :class="{ disabledButton: !inventory }"
        >
          Add to Cart
        </button>
        <button
          class="mt-6 bg-gray-500!"
          @click="removeFromCart"
          :disabled="!cart"
          :class="{ disabledButton: !cart }"
        >
          Remove from Cart
        </button>
      </div>
    </div>
  </div>
</template>

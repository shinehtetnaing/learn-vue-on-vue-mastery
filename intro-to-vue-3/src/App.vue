<script setup>
import { ref } from "vue";
import ProductDisplay from "./components/ProductDisplay.vue";

const cart = ref([]);

const premium = ref(true);

const updateCart = (id) => {
  cart.value.push(id);
};

const removeFromCart = (id) => {
  const index = cart.value.indexOf(id);
  if (index !== -1) {
    cart.value.splice(index, 1);
  }
};
</script>

<template>
  <nav class="w-full h-20 bg-green-300 px-8 flex justify-end items-center">
    <div
      class="rounded-lg border-2 border-gray-950 flex items-center justify-center text-xl font-semibold text-black p-5 h-10"
    >
      Cart ({{ cart.length }})
    </div>
  </nav>
  <ProductDisplay
    :premium="premium"
    :cart="cart"
    @add-to-cart="updateCart"
    @remove-from-cart="removeFromCart"
  ></ProductDisplay>
</template>

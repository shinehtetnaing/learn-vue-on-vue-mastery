<script setup>
import { computed, ref } from "vue";
import socksGreenImage from "../assets/images/socks_green.jpeg";
import socksBlueImage from "../assets/images/socks_blue.jpeg";

const props = defineProps({
  premium: {
    type: Boolean,
    required: true,
  },
  cart: {
    type: Array,
  },
});

const emit = defineEmits(["add-to-cart", "remove-from-cart"]);

const product = ref("Socks");
const brand = ref("Vue Mastery");
const description = ref("A pair of warm, fuzzy socks");
const selectedVarient = ref(0);

const varients = ref([
  { id: 1, color: "green", image: socksGreenImage, quantity: 50 },
  { id: 2, color: "blue", image: socksBlueImage, quantity: 0 },
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

const title = computed(() => {
  return brand.value + " " + product.value;
});

const image = computed(() => {
  return varients.value[selectedVarient.value].image;
});

const inventory = computed(() => {
  return varients.value[selectedVarient.value].quantity;
});

const shipping = computed(() => {
  return props.premium ? "Free" : "$2.99";
});

const addToCart = () =>
  emit("add-to-cart", varients.value[selectedVarient.value].id);

const removeFromCart = () => {
  // if (cart.value >= 1) {
  //   cart.value -= 1;
  // }
  emit("remove-from-cart", varients.value[selectedVarient.value].id);
};

const updateVarient = (index) => {
  selectedVarient.value = index;
};
</script>

<template>
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
        <h1 class="text-5xl/tight mb-5">{{ title }}</h1>
        <p class="text-xl mb-3">{{ description }}</p>
        <p class="text-lg mb-3">Shipping: {{ shipping }}</p>
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
              v-for="(varient, index) in varients"
              :key="varient.id"
              class="before:content-['⬤'] before:mr-2 before:text-3xl flex items-center capitalize"
              :class="listColor(varient.color)"
              @mouseover="updateVarient(index)"
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
          :disabled="!cart.length"
          :class="{ disabledButton: !cart.length }"
        >
          Remove from Cart
        </button>
      </div>
    </div>
  </div>
</template>

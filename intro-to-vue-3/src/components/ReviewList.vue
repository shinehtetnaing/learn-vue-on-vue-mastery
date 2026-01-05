<script setup>
defineProps({
  reviews: {
    type: Array,
    required: true,
  },
});
</script>

<template>
  <div class="w-full md:w-1/2">
    <h3 class="text-3xl mb-5">Reviews</h3>

    <ul class="space-y-3">
      <li
        v-for="(review, index) in reviews"
        :key="index"
        class="border-b border-green-300 pb-4"
      >
        <span class="inline-block mb-3 text-lg font-semibold"
          >{{ review.name }} gave this {{ review.rating }} stars!</span
        >

        <p class="">"{{ review.content }}"</p>
      </li>
    </ul>
  </div>
</template>

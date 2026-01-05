<script setup>
import { reactive } from "vue";

const emit = defineEmits(["review-submitted"]);

const review = reactive({
  name: "",
  content: "",
  rating: null,
});

const onSubmit = () => {
  if (review.name === "" || review.content === "" || review.rating === null) {
    alert("Please fill out all fields before submitting your review.");
    return;
  }

  const productReview = {
    name: review.name,
    content: review.content,
    rating: review.rating,
  };

  emit("review-submitted", productReview);

  review.name = "";
  review.content = "";
  review.rating = null;
};
</script>

<template>
  <div class="w-full md:w-1/2">
    <form @submit.prevent="onSubmit">
      <h3 class="text-3xl mb-5">Leave a Review</h3>

      <div class="space-y-3">
        <div>
          <label for="name" class="block text-sm/6 font-medium text-white"
            >Name</label
          >
          <div class="mt-2">
            <div
              class="flex items-center rounded-md bg-white/5 outline-1 -outline-offset-1 outline-gray-600 has-[input:focus-within]:outline-2 has-[input:focus-within]:-outline-offset-2 has-[input:focus-within]:outline-green-300"
            >
              <input
                id="name"
                type="text"
                name="name"
                v-model="review.name"
                placeholder="Enter your name"
                class="block min-w-0 grow py-2.5 px-3 text-base text-white placeholder:text-gray-500 focus:outline-none sm:text-sm/6"
              />
            </div>
          </div>
        </div>

        <div>
          <label for="review" class="block text-sm/6 font-medium text-white"
            >Review</label
          >
          <div class="mt-2">
            <div
              class="flex items-center rounded-md bg-white/5 outline-1 -outline-offset-1 outline-gray-600 focus-within:outline-2 focus-within:-outline-offset-2 focus-within:outline-green-300"
            >
              <textarea
                id="review"
                name="review"
                v-model="review.content"
                rows="4"
                class="block min-w-0 grow py-2.5 px-3 text-base text-white placeholder:text-gray-500 focus:outline-none sm:text-sm/6"
              ></textarea>
            </div>
          </div>
        </div>

        <div>
          <label for="rating" class="block text-sm/6 font-medium text-white"
            >Rating</label
          >
          <div class="mt-2">
            <div
              class="flex items-center rounded-md bg-white/5 outline-1 -outline-offset-1 outline-gray-600 focus-within:outline-2 focus-within:-outline-offset-2 focus-within:outline-green-300"
            >
              <select
                id="rating"
                name="rating"
                v-model.number="review.rating"
                class="block min-w-0 grow py-2.5 px-3 mr-1 text-base text-white placeholder:text-gray-500 focus:outline-none sm:text-sm/6"
              >
                <option class="bg-black">5</option>
                <option class="bg-black">4</option>
                <option class="bg-black">3</option>
                <option class="bg-black">2</option>
                <option class="bg-black">1</option>
              </select>
            </div>
          </div>
        </div>

        <button type="submit" value="Submit" class="mt-3">Submit</button>
      </div>
    </form>
  </div>
</template>

<template>
  <router-link
    :to="`/item-detail/${item.id}`"
    class="block rounded-md w-full mb-3"
  >
    <div
      class="rounded-md w-full p-4 flex cursor-pointer bg-white dark:bg-neutral-800 border border-gray-200 dark:border-neutral-700 hover:bg-gray-100 hover:border-gray-300 dark:hover:bg-neutral-700/50 dark:hover:border-neutral-600 transition-all duration-200"
    >
      <img
        :src="item.img_url || 'https://placehold.co/150x150?text=No+Image'"
        alt="item photo"
        class="w-24 h-24 object-cover rounded-md flex-shrink-0 border border-gray-300 dark:border-neutral-600"
      />

      <div class="ml-4 flex flex-col justify-between flex-1 min-w-0">
        <h2
          class="font-semibold text-lg text-neutral-800 dark:text-neutral-100 truncate transition-colors"
        >
          {{ item.title }}
        </h2>
        <h3
          class="text-orange-600 dark:text-orange-400 font-bold text-xl mt-1 transition-colors"
        >
          {{ formatPrice(item.price) }} SEK
        </h3>
        <h3 class="text-neutral-700 dark:text-neutral-300 transition-colors">
          {{ item.name }}
        </h3>
        <address
          class="text-gray-500 dark:text-neutral-400 text-sm mt-1 not-italic truncate transition-colors"
        >
          {{ item.location }}
        </address>
        <p
          class="text-gray-700 dark:text-neutral-300 mt-2 line-clamp-2 text-sm transition-colors"
        >
          {{ item.desc }}
        </p>
        <time
          class="text-xs text-gray-400 dark:text-neutral-500 mt-1 block transition-colors"
        >
          {{ format(new Date(item.created_at), "yyyy-MM-dd") }}
        </time>
      </div>
    </div>
  </router-link>
</template>

<script setup>
import { format } from "date-fns";

defineProps({
  item: Object,
});

const formatPrice = (price) => {
  if (!price) return "-";
  return price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
};
</script>

<style scoped></style>

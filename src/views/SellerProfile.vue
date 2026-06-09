<template>
  <div class="max-w-md mx-auto p-6 space-y-6">
    <section class="border-b border-gray-200 dark:border-neutral-800 pb-4">
      <h1 class="text-2xl font-extrabold text-gray-950 dark:text-neutral-100">
        {{ sellerName }}'s Shop
      </h1>
      <p class="text-sm text-gray-500 dark:text-neutral-400 mt-1">
        Check out all items posted by this seller
      </p>
    </section>

    <section class="space-y-4">
      <h3 class="font-semibold text-gray-700 dark:text-neutral-300">
        Posted Items ({{ sellerItems.length }})
      </h3>

      <div class="space-y-3">
        <div
          v-for="item in sellerItems"
          :key="item.id"
          class="border border-gray-100 dark:border-neutral-800/60 p-4 rounded-md bg-white dark:bg-neutral-900 shadow-sm transition-colors duration-300"
        >
          <router-link :to="`/item-detail/${item.id}`" class="block">
            <h4
              class="font-bold text-orange-600 dark:text-orange-500 hover:underline"
            >
              {{ item.title }}
            </h4>
            <p class="text-sm text-gray-600 dark:text-neutral-300 mt-1">
              {{ item.price.toLocaleString() }} SEK
            </p>
          </router-link>
        </div>

        <p
          v-if="sellerItems.length === 0"
          class="text-gray-400 dark:text-neutral-500 text-sm"
        >
          No items found.
        </p>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import supabase from "../supabase";

const route = useRoute();
const sellerId = route.params.sellerId;

const sellerName = ref("Seller");
const sellerItems = ref([]);

onMounted(async () => {
  const { data: userData } = await supabase
    .from("user_table")
    .select("name")
    .eq("id", sellerId)
    .single();

  if (userData) {
    sellerName.value = userData.name;
  }

  const { data: itemsData, error } = await supabase
    .from("item_posts")
    .select()
    .eq("author", sellerId);

  if (!error && itemsData) {
    sellerItems.value = itemsData;
  }
});
</script>

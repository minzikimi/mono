<template>
  <nav
    v-if="
      currentPath !== '/' &&
      currentPath !== '/signup' &&
      currentPath !== '/login'
    "
    class="w-full bg-white dark:bg-neutral-800 border-t border-[#E5E5EA] dark:border-neutral-700 flex justify-around items-center h-20 z-40 transition-colors duration-300"
  >
    <router-link
      v-for="tab in tabs"
      :key="tab.path"
      :to="tab.path"
      class="flex flex-col items-center justify-center text-sm text-gray-400 dark:text-neutral-500 flex-1 h-full cursor-pointer transition-colors duration-150"
      active-class="text-orange-500 dark:text-orange-400 font-semibold"
      exact
    >
      <Icon :icon="tab.icon" width="26" height="26" />
      <span class="mt-1 tracking-tight">{{ tab.label }}</span>
    </router-link>
  </nav>
</template>

<script setup>
import { Icon } from "@iconify/vue";
import { useRoute } from "vue-router";
import { computed } from "vue";

const tabs = [
  { path: "/item-listing", label: "Explore", icon: "mdi:compass-outline" },
  { path: "/chat-list", label: "Chat", icon: "mdi:chat-outline" },
  { path: "/profile", label: "Profile", icon: "teenyicons:user-circle-solid" },
];

const route = useRoute();
const currentPath = computed(() => route.path);
</script>

<script setup>
import { onMounted } from "vue";
import { useThemeStore } from "./stores/theme";
import NavBar from "./components/NavBar.vue";
import TabBar from "./components/TabBar.vue";

const themeStore = useThemeStore();

onMounted(() => {
  themeStore.initTheme();
});
</script>

<template>
  <div class="w-full min-h-screen bg-[#F5F5F7] flex justify-center">
    <div
      class="max-w-md w-full min-h-screen bg-white dark:bg-neutral-800 border-x border-[#E5E5EA] dark:border-neutral-700 flex flex-col relative transition-colors duration-300"
    >
      <NavBar />

      <main
        class="flex-1 w-full pb-16 bg-white dark:bg-neutral-800 flex flex-col transition-colors duration-300"
      >
        <router-view />
      </main>

      <TabBar />
    </div>
  </div>
</template>

<style scoped></style>

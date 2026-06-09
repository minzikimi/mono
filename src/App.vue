<template>
  <div
    class="w-full h-[100dvh] bg-[#F5F5F7] dark:bg-neutral-900 flex justify-center overflow-hidden transition-colors duration-300"
  >
    <div
      class="max-w-md w-full h-full bg-white dark:bg-neutral-800 border-x border-[#E5E5EA] dark:border-neutral-700 flex flex-col relative overflow-hidden"
    >
      <NavBar class="shrink-0" />

      <main class="flex-1 w-full bg-white dark:bg-neutral-800 overflow-y-auto">
        <router-view />
      </main>

      <TabBar class="shrink-0" />
    </div>
  </div>
</template>

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

<style scoped>
:global(html),
:global(body) {
  margin: 0;
  padding: 0;
  height: 100dvh;
  overflow: hidden;
}
</style>

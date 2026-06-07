<script setup>
import NavBar from "./components/NavBar.vue";
import TabBar from "./components/TabBar.vue";
</script>

<template>
  <div class="w-full min-h-screen bg-[#F5F5F7] flex justify-center">
    <div
      class="max-w-md w-full min-h-screen bg-white border-x border-[#E5E5EA] flex flex-col relative"
      style="font-family: &quot;Host Grotesk&quot;, sans-serif"
    >
      <NavBar />

      <main class="flex-1 w-full pb-16">
        <router-view />
      </main>

      <TabBar />
    </div>
  </div>
</template>

<style scoped></style>

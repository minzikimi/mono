<template>
  <div
    class="w-full h-full flex flex-col justify-center items-center bg-white dark:bg-neutral-800 px-4 relative overflow-hidden transition-colors duration-300"
  >
    <button
      @click="themeStore.toggleDarkMode"
      class="absolute top-6 right-6 z-50 text-neutral-700 dark:text-neutral-200 p-2 hover:opacity-80 active:scale-95 transition-all cursor-pointer flex items-center justify-center bg-gray-100 dark:bg-neutral-700 rounded-full shadow-sm"
      aria-label="Toggle Dark Mode"
    >
      <Icon
        :icon="
          themeStore.isDarkMode
            ? 'material-symbols:wb-sunny-outline'
            : 'material-symbols:dark-mode-outline'
        "
        width="24"
        height="24"
      />
    </button>

    <!-- bg-circles -->
    <div class="absolute inset-0 pointer-events-none overflow-hidden">
      <div
        class="absolute w-38 h-38 bg-orange-500 dark:bg-orange-400 rounded-full opacity-30 dark:opacity-25 animate-moveCircle1 transition-colors duration-300"
      ></div>
      <div
        class="absolute w-26 h-26 bg-orange-500 dark:bg-orange-400 rounded-full opacity-20 dark:opacity-20 animate-moveCircle2 transition-colors duration-300"
      ></div>
    </div>

    <h1
      class="text-6xl font-extrabold mb-10 text-neutral-700 dark:text-neutral-100 tracking-wide z-10 transition-colors"
    >
      MoNoモノ
    </h1>

    <router-link
      to="/signup"
      class="rounded-md w-full max-w-xs py-4 mb-6 bg-orange-500 hover:bg-orange-600 text-white text-xl font-semibold shadow inline-block text-center z-10 transition-colors"
    >
      Start
    </router-link>

    <div class="login-button z-10 text-center">
      <h3 class="text-neutral-700 dark:text-neutral-300 transition-colors">
        Already a member?
      </h3>
      <router-link
        to="/login"
        class="text-orange-500 dark:text-orange-400 font-semibold"
      >
        Login
      </router-link>
    </div>
  </div>
</template>

<script setup>
import { Icon } from "@iconify/vue";
import { useThemeStore } from "../stores/theme";

const themeStore = useThemeStore();
</script>

<style scoped>
@keyframes moveCircle1 {
  0%,
  100% {
    transform: translateX(-15%);
  }
  50% {
    transform: translateX(15%);
  }
}
@keyframes moveCircle2 {
  0%,
  100% {
    transform: translateX(10%);
  }
  50% {
    transform: translateX(-10%);
  }
}
.animate-moveCircle1 {
  animation: moveCircle1 6s ease-in-out infinite;
  top: 18%;
  left: 22%;
}
.animate-moveCircle2 {
  animation: moveCircle2 8s ease-in-out infinite;
  top: 22%;
  right: 28%;
}
</style>

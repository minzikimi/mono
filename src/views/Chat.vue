<template>
  <div
    class="absolute inset-0 bg-orange-500 bg-opacity-40 flex items-center justify-center z-50 p-4"
  >
    <div
      class="bg-white w-full max-w-[calc(100%-2rem)] rounded-2xl shadow-lg flex flex-col overflow-hidden"
    >
      <!-- Header -->
      <div
        class="p-4 border-b border-[#E5E5EA] flex justify-between items-center"
      >
        <h2 class="font-bold text-lg text-neutral-800">Chat</h2>
        <button
          @click.prevent.stop="$emit('close')"
          class="text-gray-400 hover:text-black cursor-pointer text-sm"
        >
          ✕
        </button>
      </div>

      <div class="p-6 flex-1 bg-white">
        <p class="text-neutral-500 text-center font-medium">Coming soon!</p>
      </div>
    </div>
  </div>
</template>

<script setup></script>

<style scoped></style>

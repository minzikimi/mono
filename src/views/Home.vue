<template>
  <div
    class="w-full min-h-screen flex flex-col justify-center items-center bg-white px-4 relative overflow-hidden"
  >
    <!-- bg-circles -->
    <div class="absolute inset-0 pointer-events-none overflow-hidden">
      <div
        class="absolute w-48 h-48 bg-orange-500 rounded-full opacity-30 animate-moveCircle1"
      ></div>
      <div
        class="absolute w-36 h-36 bg-orange-500 rounded-full opacity-20 animate-moveCircle2"
      ></div>
    </div>

    <h1
      class="text-6xl font-extrabold mb-10 text-neutral-700 tracking-wide z-10"
    >
      MoNoモノ
    </h1>

    <router-link
      to="/signup"
      class="rounded-md w-full max-w-xs py-4 mb-6 bg-orange-500 hover:bg-orange-600 text-white text-xl font-semibold shadow inline-block text-center z-10"
    >
      Start
    </router-link>

    <div class="login-button z-10 text-center">
      <h3 class="text-neutral-700">Already a member?</h3>
      <router-link to="/login" class="text-orange-500"> Login </router-link>
    </div>
  </div>
</template>

<script setup></script>

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

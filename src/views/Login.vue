<template>
  <Spinner :visible="isLoading" text="just a moment..." />
  <div
    class="w-full h-full flex flex-col justify-center items-center bg-white dark:bg-neutral-800 px-4 transition-colors duration-300"
  >
    <form class="w-full max-w-xs" @submit.prevent="handleLogin">
      <div class="relative flex items-center justify-center mb-10 w-full">
        <button
          type="button"
          @click.prevent="router.back()"
          class="absolute left-0 text-xl p-2 text-neutral-600 dark:text-neutral-400 hover:text-black dark:hover:text-white cursor-pointer transition-colors"
        >
          ✕
        </button>
        <h1
          class="text-6xl font-extrabold text-neutral-700 dark:text-neutral-100 tracking-wide transition-colors"
        >
          Login
        </h1>
      </div>

      <div class="mb-4">
        <label
          for="email"
          class="block mb-1 text-gray-700 dark:text-neutral-300 font-semibold text-sm transition-colors"
          >Email</label
        >
        <input
          type="email"
          id="email"
          placeholder="Enter your email"
          required
          v-model="email"
          class="rounded-md w-full px-4 py-3 border border-gray-200 dark:border-neutral-600 bg-white dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400 focus:outline-none focus:border-blue-400 dark:focus:border-blue-500 text-base transition-all"
        />
      </div>

      <div class="mb-6">
        <label
          for="password"
          class="block mb-1 text-gray-700 dark:text-neutral-300 font-semibold text-sm transition-colors"
          >Password</label
        >
        <input
          type="password"
          id="password"
          required
          placeholder="Enter your password"
          v-model="password"
          class="rounded-md w-full px-4 py-3 border border-gray-200 dark:border-neutral-600 bg-white dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400 focus:outline-none focus:border-blue-400 dark:focus:border-blue-500 text-base transition-all"
        />
      </div>

      <button
        type="submit"
        class="rounded-md w-full py-3 bg-orange-500 hover:bg-orange-600 text-white font-semibold text-base shadow active:scale-[0.98] transition-all cursor-pointer"
      >
        Log In
      </button>
    </form>
  </div>
</template>

<script setup>
import { useRouter } from "vue-router";
import supabase from "../supabase";
import { ref } from "vue";
import Spinner from "../components/Spinner.vue";

const email = ref("");
const password = ref("");

const router = useRouter();
const isLoading = ref(false);

const handleLogin = async () => {
  console.log(email.value, password.value);
  isLoading.value = true;
  const { data, error } = await supabase.auth.signInWithPassword({
    email: email.value,
    password: password.value,
  });
  isLoading.value = false;

  if (error) {
    alert(error.message);
  } else {
    // alert(" login successful");
    console.log(data);
    router.push("/item-listing");
  }
};
</script>

<style></style>

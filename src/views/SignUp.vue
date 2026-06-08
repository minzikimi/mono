<template>
  <Spinner :visible="isLoading" text="just a moment..." />
  <div
    class="w-full h-full flex flex-col justify-center px-6 py-10 bg-white dark:bg-neutral-800 text-neutral-700 dark:text-neutral-200 transition-colors duration-300"
  >
    <h1
      class="text-4xl font-bold mb-8 text-center text-neutral-700 dark:text-neutral-100 transition-colors"
    >
      Join MoNo
    </h1>

    <form @submit.prevent="handleSignup" class="space-y-6">
      <input
        type="email"
        v-model="email"
        placeholder="Enter your Hyper Island email"
        required
        class="w-full px-4 py-3 border border-gray-200 dark:border-neutral-600 rounded-md bg-white dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-orange-500"
      />

      <input
        type="password"
        v-model="password"
        placeholder="Enter your password"
        required
        class="w-full px-4 py-3 border border-gray-200 dark:border-neutral-600 rounded-md bg-white dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-orange-500"
      />

      <input
        type="tel"
        v-model="tel"
        placeholder="+46 00 0000 0000"
        required
        class="w-full px-4 py-3 border border-gray-200 dark:border-neutral-600 rounded-md bg-white dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-orange-500"
      />

      <input
        type="text"
        v-model="name"
        placeholder="Enter your name"
        required
        class="w-full px-4 py-3 border border-gray-200 dark:border-neutral-600 rounded-md bg-white dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-orange-500"
      />

      <input
        type="text"
        v-model="location"
        placeholder="Enter your location"
        required
        class="w-full px-4 py-3 border border-gray-200 dark:border-neutral-600 rounded-md bg-white dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-orange-500"
      />

      <textarea
        v-model="text"
        placeholder="Self introduction"
        rows="4"
        class="w-full px-4 py-3 border border-gray-200 dark:border-neutral-600 rounded-md bg-white dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400 resize-y focus:outline-none focus:ring-2 focus:ring-orange-500"
      ></textarea>
      <button
        type="submit"
        class="cursor-pointer w-full py-3 bg-orange-500 text-white font-semibold rounded-md hover:bg-orange-600 active:scale-[0.99] transition-all"
      >
        Sign Up
      </button>

      <p
        class="mt-6 text-center text-gray-600 dark:text-neutral-400 transition-colors"
      >
        Already a member?
        <router-link
          to="/login"
          class="text-orange-500 dark:text-orange-400 underline ml-1"
          >Login</router-link
        >
      </p>
    </form>

    <Modal
      :show="showModal"
      title="Signup Complete!"
      message="Your account has been created successfully. Please log in to continue."
      confirmText="Go to Login"
      @close="showModal = false"
      @confirm="router.push('/login')"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
import supabase from "../supabase";
import Spinner from "../components/Spinner.vue";
import { useRouter } from "vue-router";
import Modal from "../components/Modal.vue";

const router = useRouter();
const showModal = ref(false);

const email = ref("");
const password = ref("");
const tel = ref("");
const name = ref("");
const text = ref("");
const location = ref("");

const isLoading = ref(false);

const handleSignup = async () => {
  if (!email.value.endsWith("@hyperisland.se")) {
    alert("Only HI emails are allowed.");
    return;
  }

  isLoading.value = true;

  const { data, error } = await supabase.auth.signUp({
    email: email.value,
    password: password.value,
  });

  if (error) {
    alert(error.message);
  } else {
    // console.log("sign up sucessful");
    console.log(data);

    const { error } = await supabase.from("user_table").insert({
      tel: tel.value,
      text: text.value,
      name: name.value,
      location: location.value,
    });
    if (error) {
      alert("error");
      console.log(error);
    } else {
      isLoading.value = false;
      showModal.value = true;
      // router.push("/login");
    }
  }
};
</script>

<style scoped></style>

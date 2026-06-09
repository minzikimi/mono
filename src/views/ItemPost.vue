<template>
  <Spinner :visible="isLoading" text="Just a moment, we're posting..." />
  <!--  -->
  <div
    class="overflow-y: auto; max-w-md w-full flex flex-col justify-start items-center bg-gray-50 dark:bg-neutral-800 p-4 overflow-auto transition-colors duration-300"
  >
    <form
      v-if="isLogin"
      @submit.prevent="handleSubmit"
      class="space-y-6 bg-white dark:bg-neutral-800 p-6 rounded-none w-full transition-colors duration-300"
    >
      <label
        for="photo"
        class="border-2 rounded-md border-dashed border-gray-300 dark:border-neutral-600 cursor-pointer bg-center bg-cover mb-2 flex flex-col items-center justify-center text-neutral-300 dark:text-neutral-500 bg-gray-50 dark:bg-neutral-700/50"
        :style="
          previewImage
            ? `background-image: url('${previewImage}'); width: 150px; height: 150px;`
            : 'width: 150px; height: 150px;'
        "
      >
        <template v-if="!previewImage">
          <!-- Camera Icon -->
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="w-12 h-12 text-gray-400 dark:text-neutral-500"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke="currentColor"
              stroke-width="1.5"
              d="M5 7l1.5-2h11L19 7M3 7h18a2 2 0 012 2v9a2 2 0 01-2 2H3a2 2 0 01-2-2V9a2 2 0 012-2zm9 3a4 4 0 100 8 4 4 0 000-8zm0 5.8a1.8 1.8 0 110-3.6 1.8 1.8 0 010 3.6z"
            />
          </svg>
          <div class="text-neutral-400 dark:text-neutral-500 text-sm">
            Add a photo
          </div>
        </template>
      </label>

      <input
        @change="onFileChange"
        type="file"
        id="photo"
        accept="image/*"
        class="hidden"
      />

      <!-- Title -->
      <div class="flex flex-col">
        <label
          for="title"
          class="mb-2 font-semibold text-gray-700 dark:text-neutral-200"
          >Title</label
        >
        <input
          id="title"
          type="text"
          v-model="title"
          required
          placeholder="Please provide a concise title for your item"
          class="border border-gray-400 dark:border-neutral-600 px-4 py-2 focus:outline-none focus:ring-2 focus:ring-orange-500 bg-gray-50 dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400"
        />
      </div>
      <div class="flex flex-col">
        <label
          for="price"
          class="mb-2 font-semibold text-gray-700 dark:text-neutral-200"
          >Price</label
        >
        <input
          id="price"
          type="number"
          v-model="price"
          required
          placeholder="Price"
          class="border border-gray-400 dark:border-neutral-600 px-4 py-2 focus:outline-none focus:ring-2 focus:ring-orange-500 bg-gray-50 dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400"
        />
      </div>
      <div class="flex flex-col">
        <label
          for="description"
          class="mb-2 font-semibold text-gray-700 dark:text-neutral-200"
          >Description</label
        >
        <textarea
          id="description"
          v-model="description"
          required
          placeholder="Detailed item description"
          rows="4"
          class="border border-gray-400 dark:border-neutral-600 px-4 py-2 focus:outline-none focus:ring-2 focus:ring-orange-500 bg-gray-50 dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400 resize-none"
        />
      </div>
      <div class="flex flex-col">
        <label
          for="location"
          class="mb-2 font-semibold text-gray-700 dark:text-neutral-200"
          >Location</label
        >
        <input
          id="location"
          type="text"
          v-model="location"
          required
          placeholder="City, district, or neighborhood"
          class="border border-gray-400 dark:border-neutral-600 px-4 py-2 focus:outline-none focus:ring-2 focus:ring-orange-500 bg-gray-50 dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400"
        />
      </div>
      <div class="flex flex-col">
        <label
          for="tel"
          class="mb-2 font-semibold text-gray-700 dark:text-neutral-200"
          >Phone number</label
        >
        <input
          id="tel"
          type="tel"
          v-model="tel"
          required
          placeholder="tel number"
          class="border border-gray-400 dark:border-neutral-600 px-4 py-2 focus:outline-none focus:ring-2 focus:ring-orange-500 bg-gray-50 dark:bg-neutral-700 text-neutral-900 dark:text-neutral-100 placeholder-gray-400"
        />
      </div>
      <button
        type="submit"
        class="w-full py-4 bg-orange-500 text-white font-semibold hover:bg-orange-600 transition rounded-none cursor-pointer"
      >
        Post Item
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useAuth } from "../auth/useAuth";
import { onMounted } from "vue";
import supabase from "../supabase";
import Spinner from "../components/Spinner.vue";
import { useRouter } from "vue-router";

const title = ref("");
const price = ref("");
const description = ref("");
const location = ref("");
const tel = ref("");
const previewImage = ref("");
const img_url = ref("");
//첨부한사진은 스토리지에 저장하고 유알엘을 저장
const { isLogin, user, updateUserState } = useAuth();

const isLoading = ref(false);
const router = useRouter();

onMounted(async () => {
  await updateUserState();
  console.log("auth 정보", isLogin.value, user.value);
});

let file = null;
const onFileChange = (e) => {
  file = e.target.files[0];
  console.log(file);

  if (file) {
    previewImage.value = URL.createObjectURL(file);
    console.log(previewImage.value);
  }
};

const uploadImage = async () => {
  const { data, error } = await supabase.storage
    .from("images")
    .upload(file.name, file, {
      cacheControl: "3600",
      upsert: false,
    });

  if (error) {
    console.log("Upload Error:", error);
    alert("UploadError: " + error.message);
  } else {
    console.log("uploaded file :", data);
    //itemposts테이블에 이미지 url를 저장하려면 storage에 저장된 이미지의 경로를 알아야됨
    //이미지 유알엘 가져오기
    const { data: imgData } = supabase.storage
      .from("images")
      .getPublicUrl(file.name);
    console.log("file url", imgData.publicUrl);

    //테이블에 저장할 image변수
    img_url.value = imgData.publicUrl;
  }
};

const handleSubmit = async () => {
  isLoading.value = true;

  if (previewImage.value) {
    await uploadImage();
  }
  const { error } = await supabase.from("item_posts").insert({
    title: title.value,
    price: price.value,
    description: description.value,
    location: location.value,
    tel: tel.value,
    // user_id: user.value.id,
    img_url: img_url.value,
  });
  if (error) {
    console.log(error);
    alert(error);
  } else {
    alert("posted!!");
    router.push("/item-listing");
  }
  isLoading.value = false;
};
</script>

<style scoped></style>

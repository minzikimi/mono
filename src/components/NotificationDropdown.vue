<template>
  <div
    v-if="show"
    class="absolute left-3 mt-2 w-64 bg-green-600 dark:bg-green-700 border border-green-500 rounded-lg shadow-xl z-50 max-h-64 overflow-y-auto transition-all duration-200"
  >
    <p
      v-if="notifications.length === 0"
      class="p-4 text-center text-sm text-green-100/90"
    >
      No notifications
    </p>
    <ul v-else class="divide-y divide-green-500/50">
      <li
        v-for="(note, idx) in notifications"
        :key="idx"
        class="px-4 py-3 hover:bg-green-500/30 cursor-pointer transition-colors"
        @click="goToItem(note.postId)"
      >
        <p class="text-sm font-medium text-white leading-snug">
          {{ note.message }}
        </p>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { useNotificationStore } from "../stores/notification";
import { useRouter } from "vue-router";
import { computed } from "vue";

const props = defineProps({
  show: Boolean,
});

const notificationStore = useNotificationStore();
const notifications = computed(() => notificationStore.notifications);

const router = useRouter();
function goToItem(postId) {
  router.push(`/item-detail/${postId}`);
}
</script>

<style scoped></style>

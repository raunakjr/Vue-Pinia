<template>
  <form @submit.prevent="HandleSubmit" class="flex flex-col items-center my-5">
    <input
      class="p-5 border-2 border-gray-600 rounded-lg my-3 w-1/2"
      type="text"
      placeholder="Enter task title"
      v-model="title"
    />

    <div class="flex items-center space-x-2 w-1/2 text-3xl">
      <label class="p-5 border-2 border-gray-600 rounded-lg my-3 w-1/2">
        Mark as Fav</label
      >
      <input
        class="p-5 border-2 border-gray-600 rounded-lg my-3 w-1/2"
        type="checkbox"
        v-model="isFav"
      />
    </div>

    <button class="p-5 border-2 border-gray-600 rounded-lg my-3 w-1/5">
      Add Task
    </button>
  </form>
</template>

<script setup>
import { useTaskStore } from "@/stores/TaskStore";
import { ref } from "vue";
const taskStore = useTaskStore();
const title = ref("");
const id = ref("");
const isFav = ref(false);

const HandleSubmit = () => {
  if (title.value) {
    console.log(title.value, id.value, isFav.value);
    taskStore.addTask({
      title: title.value,
      id: Math.floor(Math.random() * 10000),
      isFav: isFav.value,
    });
    title.value = "";
  }
};
</script>

<style lang="scss" scoped></style>

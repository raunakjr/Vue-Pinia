<template>
  <div
    class="px-5 py-2 bg-gray-300 border-2 border-gray-600 rounded-lg my-3 w-1/2 flex justify-between items-center mx-auto"
  >
    <h2 class="text-2xl">{{ title }}</h2>
    <div class="flex space-x-2">
      <i class="material-icons cursor-pointer text-blue-600">edit</i>
      <i
        @click="taskStore.RemoveTask(id)"
        class="material-icons cursor-pointer text-yellow-800"
        >delete</i
      >
      <i
        @click="taskStore.ToggleFav(id)"
        class="material-icons cursor-pointer"
        :class="{
          'text-red-600': task.isFav,
          'text-green-600': !task.isFav,
        }"
        >favorite</i
      >
    </div>
  </div>
</template>

<script setup>
import { useTaskStore } from "@/stores/TaskStore";
import { defineProps } from "vue";

const props = defineProps({
  task: Object,
});

const { title, id } = props.task;

const taskStore = useTaskStore();
</script>

<style lang="scss" scoped></style>

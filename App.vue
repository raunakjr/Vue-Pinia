<template>
  <main>
    <header>
      <img
        src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQWTjJR7SUzIuTRkJ972Z2lloadKBGB8K46aA&s"
        alt=""
      />
      <h1>Pinia Tasks</h1>
    </header>
    <!-- // Displaying the tasks -->

    <nav class="flex justify-center my-5 text-2xl">
      <button
        class="px-3 py-1 border-2 rounded-lg bg-gray-300 text-gray-600 cursor-pointer"
        @click="filter = 'all'"
      >
        All tasks
      </button>
      <button
        class="px-3 py-1 border-2 rounded-lg bg-gray-300 text-gray-600 cursor-pointer"
        @click="filter = 'fav'"
      >
        Fav tasks
      </button>
    </nav>

    <div v-if="taskStore.isLoading">
      <h1 class="text-3xl text-center my-10">Loading...</h1>
    </div>

    <div v-else>
      <div v-if="filter === 'all'">
        <h1 class="text-3xl text-center my-10">
          You have total {{ taskStore.TotalCount }} tasks
        </h1>
        <div v-for="task in taskStore.tasks" :key="task.id">
          <Taskdetails :task="task" />
        </div>
      </div>
      <div v-else-if="filter === 'fav'">
        <h1 class="text-3xl text-center my-10">
          You have total {{ taskStore.FavCount }} Fav tasks
        </h1>
        <div v-for="task in taskStore.getFavTasks" :key="task.id">
          <Taskdetails :task="task" />
        </div>
      </div>
    </div>
  </main>
  <TaskForm />
</template>

<script setup>
import Taskdetails from "./components/Taskdetails.vue";
import TaskForm from "./components/TaskForm.vue";
import { useTaskStore } from "./stores/TaskStore";
import { onMounted, ref, watchEffect } from "vue";
const filter = ref("all");
const taskStore = useTaskStore();

onMounted(() => {
  taskStore.getTasks();
});
</script>

<style lang="scss" scoped></style>

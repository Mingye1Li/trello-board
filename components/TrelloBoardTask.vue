<script setup lang="ts">
import type { Task } from "~/types";
defineProps<{
  task: Task;
}>();
</script>

<template>
  <div
    :title="task.createfAt.toLocaleDateString()"
    class="task bg-white p-2 mb-2 rounded shadow-sm max-w-[250px] flex"
  >
    <DragHandle class="pr-2" />
    <span>{{ task.title }}</span>
  </div>
</template>
<style>
.sortable-chosen.task {
  transform: rotate(5deg);
}

.sortable-ghost.task {
  position: relative;
  opacity: 1;
  transform: rotate(5deg);
}
.sortable-ghost.task::after {
  content: "";
  @apply absolute top-0 bottom-0 right-0 left-0 bg-slate-300 rounded;
}
</style>

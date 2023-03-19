<script setup lang="ts">
// import { ref } from 'vue'  is done automatically in nuxt
import type { Column, Task } from "~/types";
import { nanoid } from "nanoid";
import draggable from "vuedraggable";
import { useKeyModifier } from "@vueuse/core";
const alt = useKeyModifier("Alt");
const columns = ref<Column[]>([
  {
    id: nanoid(),
    title: "Backlog",
    tasks: [
      {
        id: nanoid(),
        title: "Task 1",
        createfAt: new Date(),
      },
      {
        id: nanoid(),
        title: "Task 2",
        createfAt: new Date(),
      },
      {
        id: nanoid(),
        title: "Task 3",
        createfAt: new Date(),
      },
    ],
  },
  {
    id: nanoid(),
    title: "Todo",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "In Progress",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "QA",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "Completed",
    tasks: [],
  },
]);
</script>
<template>
  <div>
    <draggable
      v-model="columns"
      group="columns"
      item-key="id"
      :animation="300"
      handle=".drag-handle"
      class="flex gap-4 overflow-x-auto items-start"
    >
      <template #item="{ element: column }: { element: Column }">
        <div class="column p-5 bg-gray-200 rounded min-w-[250px]">
          <header class="font-bold mb-4">
            <DragHandle />
            {{ column.title }}
          </header>
          <draggable
            v-model="column.tasks"
            :group="{ name: 'tasks', pull: alt ? 'clone' : true }"
            item-key="id"
            :animation="300"
            handle=".drag-handle"
          >
            <template #item="{ element: task }: { element: Task }">
              <TrelloBoardTask :key="task.id" :task="task" />
            </template>
          </draggable>

          <footer>
            <button class="text-gray-500">+ Add a card</button>
          </footer>
        </div>
      </template>
    </draggable>
  </div>
</template>

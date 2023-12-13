<script setup lang="ts">
import { PhCircle, PhCheckCircle } from "@phosphor-icons/vue"

import TaskForm from "./TaskForm.vue";
import { useTaskStore } from "@/stores/task"
import { useListStore } from "@/stores/list";
import { storeToRefs } from "pinia"

const tasksStore = useTaskStore()
const listStore = useListStore()

const { listTasks, total, completedTasks } = storeToRefs(tasksStore)
const { currentListInfo } = storeToRefs(listStore)
const { completeTask } = tasksStore
</script>

<template>
  <div class="flex flex-col h-full">
    <div class="text-3xl mb-4 font-semibold">{{ currentListInfo?.name }}</div>
    <div class="">
      <div class="taskList">
        <div class="flex flex-col gap-y-2">
          <div v-for="task in listTasks" :key="task.id" class="flex items-center bg-dark-300 rounded-md px-4 py-2.5">
            <div class="cursor-pointer mr-2" @click="completeTask(task.id)">
              <ph-circle v-show="!task.completed" :size="20" />
              <ph-check-circle v-show="task.completed" :size="20" />
            </div>
            <div :class="task.completed ? 'line-through text-white/40' : ''">
              {{ task.title }}
            </div>
          </div>

          <!-- <div class="flex justify-between">
            <div>Total: {{ total }}</div>
            <div>Done: {{ completedTasks.length + "/" + total }}</div>
          </div> -->
        </div>
      </div>

    </div>
    <TaskForm class="mt-auto" :selected-list="currentListInfo?.id" />
  </div>
</template>
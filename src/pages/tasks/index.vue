<script setup lang="ts">
import { RouterLink } from 'vue-router';
import { columns } from '@/utils/tableColumns/tasksColumns';
import { tasksWithProjectsQuery, type TasksWithProjects } from '@/utils/supaQueries';
import { useErrorStore } from '@/stores/error';

usePageStore().pageData.title = 'My Tasks'

const tasks = ref<TasksWithProjects | null>(null);

const getTasks = async () => {
  const { data, error, status } = await tasksWithProjectsQuery

  if (error) useErrorStore().setError({ error, customCode: status });

  tasks.value = data;
}

await getTasks()
</script>

<template>
    <DataTable v-if="tasks" :columns="columns" :data="tasks">
        <template #cell-name="{ cell }">
            <RouterLink :to="`/tasks/${cell.row.original.id}`">
                {{ cell.getValue() }}
            </RouterLink>
        </template>
        <template #cell-projects="{ cell }">
            <RouterLink :to="`/projects/${cell.row.original.projects?.slug}`">
                {{ cell.row.original.projects?.name }}
            </RouterLink>
        </template>
    </DataTable>
</template>

<script setup lang="ts">
import { RouterLink } from 'vue-router';
import { projectsQuery, type Projects } from '@/utils/supaQueries';
import { columns } from '@/utils/tableColumns/projectsColumns';
import { useErrorStore } from '@/stores/error';

const projects = ref<Projects | null>(null);

const getProrjects = async () => {
  const { data, error, status } = await projectsQuery

  if (error) useErrorStore().setError({ error, customCode: status });

  projects.value = data;
}

await getProrjects()

usePageStore().pageData.title = 'Projects'

</script>

<template>
    <DataTable v-if="projects" :columns="columns" :data="projects">
        <template #cell-name="{ cell }">
            <RouterLink :to="`/projects/${cell.row.original.slug}`">
                {{ cell.getValue() }}
            </RouterLink>
        </template>
    </DataTable>
</template>

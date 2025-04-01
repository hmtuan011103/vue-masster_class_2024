<script setup lang="ts">
import { RouterLink } from 'vue-router';
import { projectsQuery, type Projects } from '@/utils/supaQueries';
import { columns } from '@/utils/tableColumns/projectsColumns';

const projects = ref<Projects | null>(null);

const getProrjects = async () => {
  const { data, error } = await projectsQuery

  if (error) console.log(error);

  projects.value = data;
}

await getProrjects()

usePageStore().pageData.title = 'Projects'

</script>

<template>
    <DataTable v-if="projects" :columns="columns" :data="projects">
        <template #cell-name="{ cell }">
            <RouterLink :to="`/projects/${cell.row.original?.slug}`">
                {{ cell.getValue() }}
            </RouterLink>
        </template>
    </DataTable>
</template>

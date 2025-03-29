<script setup lang="ts">
import { Button } from '@/components/ui/button'
</script>

<template>
    <div>
        <h1>Home Page</h1>
        <RouterLink 
            :to="{ name: '/projects/[id]', params: { id: 1 } }"
        >
            Go to project 1
        </RouterLink>
        <Button>Click me</Button>
    </div> 
</template>
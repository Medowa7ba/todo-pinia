<template lang="pug">
.task
    h3 {{ task.title }}
    .icons
        i.material-icons(@click="taskStore.deleteTask(task.id)") delete
        i.material-icons(:class="{active: task.isFav}", @click="taskStore.toggleFav(task.id)") favorite
</template>
<script lang="ts" setup>
const props = defineProps(['task']);
import { useTaskStore } from '@/stores/task'
const taskStore = useTaskStore()
</script>
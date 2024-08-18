<template lang="pug">
main
  header
    img(src="https://pinia.vuejs.org/logo.svg", alt="pinia logo")
    h1 Pinia Tasks
  .new-task-form
    TaskForm
  nav.filter
    button(@click="filter = 'all'") All tasks
    button(@click="filter = 'favs'") Fav tasks
  .loading(v-if="loading") Loading tasks...
  .task-list(v-if="filter === 'all'")
    p You have {{ totalCount }} tasks left to do.
    div(v-for="task in tasks", :key="task.id")
      TaskDetails(:task="task")
  .task-list(v-if="filter === 'favs'")
    p You have {{ favCount }} tasks in your favs list.
    div(v-for="task in favs", :key="task.id")
      TaskDetails(:task="task").
  button(@click="taskStore.$reset") reset the state
</template>
<script setup lang="ts">
import TaskForm from './components/TaskForm.vue'
import TaskDetails from './components/TaskDetails.vue';
import { useTaskStore } from './stores/task';
import { storeToRefs } from 'pinia';
import { ref } from 'vue';
const taskStore = useTaskStore()
const { tasks, loading, favs, totalCount, favCount } = storeToRefs(taskStore)
taskStore.getTasks()
const filter = ref('all')
</script>
<style scoped lang="scss">

</style>

<template lang="pug">
form(@submit.prevent="handleSubmit")
  input(type="text", placeholder="I need to...", v-model="newTask")
  button Add
</template>
  
  <script lang="ts" setup>
  import { ref } from 'vue'
  import { useTaskStore } from '@/stores/task'
      const taskStore = useTaskStore()
  
      const newTask = ref('')
  
      const handleSubmit = () => {
        if (newTask.value.length > 0) {
          taskStore.addTask({
            title: newTask.value,
            isFav: false,
            id: Math.floor(Math.random() * 1000000)
          })
          newTask.value = ""
        }
      }
  </script>
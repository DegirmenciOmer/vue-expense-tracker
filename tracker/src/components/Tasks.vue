<template>
  <div>
    <div v-for="task in tasks" :key="task.id">
      <AppTask :task="task" />
    </div>
  </div>
</template>

<script>
import AppTask from './Task.vue'
export default {
  name: 'AppTasks',
  props: {
    tasks: Array,
  },
  components: {
    AppTask,
  },
}
</script>

<style></style>

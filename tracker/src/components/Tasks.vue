<template>
  <div>
    <div v-for="task in tasks" :key="task.id">
      <AppTask
        @toggle-reminder="$emit('toggle-reminder', task.id)"
        @delete-task="$emit('delete-task', task.id)"
        :task="task"
      />
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
  emits: ['delete-task', 'toggle-reminder'],
}
</script>

<style></style>

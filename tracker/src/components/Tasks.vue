<template>
  <div>
    <template v-if="tasks.length > 0">
      <div v-for="task in tasks" :key="task.id">
        <AppTask
          @toggle-reminder="$emit('toggle-reminder', task.id)"
          @delete-task="$emit('delete-task', task.id)"
          :task="task"
        />
      </div>
    </template>
    <template v-else>
      <p>No tasks found!</p>
    </template>
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

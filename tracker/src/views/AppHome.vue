<template>
  <div>
    <AddTask v-if="showAddTask" @add-task="addTask" />
    <AppTasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import AppTasks from '../components/Tasks.vue'
import AddTask from '../components/AddTask'

export default {
  name: 'AppHome',
  props: {
    showAddTask: Boolean,
  },
  components: { AppTasks, AddTask },
  methods: {
    async addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    async deleteTask(id) {
      if (confirm('Are you sure')) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    async toggleReminder(id) {
      this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      )
    },
  },
  data() {
    return { tasks: [] }
  },
  async created() {
    this.tasks = []
  },
  emits: ['delete-task'],
}
</script>

<style></style>

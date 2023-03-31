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
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: { 'Content-type': 'application/json' },
        body: JSON.stringify(task),
      })

      const data = await res.json()

      this.tasks = [...this.tasks, data]
    },
    async deleteTask(id) {
      if (confirm('Are you sure')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        })

        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert('Delete is not successful')
      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)

      const updatedTask = {
        ...taskToToggle,
        reminder: !taskToToggle.reminder,
      }

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: { 'Content-type': 'application/json' },
        body: JSON.stringify(updatedTask),
      })

      const data = await res.json()

      // this.tasks[id - 1].reminder = !this.tasks[id - 1].reminder
      // or
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      )
    },
    async fetchTasks() {
      const res = await fetch('api/tasks')

      const data = await res.json()

      return data
    },

    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`)

      const data = await res.json()

      return data
    },
  },
  data() {
    return { tasks: [] }
  },
  async created() {
    this.tasks = await this.fetchTasks()
  },
  emits: ['delete-task'],
}
</script>

<style></style>

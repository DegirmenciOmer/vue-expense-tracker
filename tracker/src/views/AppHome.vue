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
    addTask(task) {
      this.tasks = [...this.tasks, task]
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    },

    deleteTask(id) {
      if (confirm('Are you sure')) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      )
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    },
  },
  data() {
    return { tasks: [] }
  },
  async created() {
    const localTasks = localStorage.getItem('tasks')
    this.tasks = JSON.parse(localTasks) ?? []
  },
  emits: ['delete-task'],
}
</script>

<style></style>

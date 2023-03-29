<template>
  <header>
    <h1>{{ title }}</h1>
    <AppButton text="Add Task" color="green" />
  </header>
</template>

<script>
import AppButton from './Button'

export default {
  name: 'AppHeader',
  props: {
    title: String,
  },
  components: { AppButton },
}
</script>

<style>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>

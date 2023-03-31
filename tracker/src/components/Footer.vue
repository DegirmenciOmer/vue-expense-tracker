<template>
  <footer>
    <p>Copyright &copy;{{ currentYear }}</p>
    <router-link to="/about">About</router-link>
  </footer>
</template>

<script>
export default {
  name: 'AppFooter',
  data() {
    return { currentYear: new Date().getFullYear() }
  },
}
</script>

<style scoped>
a {
  color: #333;
}
footer {
  margin-top: 30px;
  text-align: center;
}
</style>

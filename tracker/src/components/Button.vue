<template>
  <button v-on:click="onClick()" :style="{ background: color }" class="btn">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: 'AppButton',
  props: {
    text: String,
    color: String,
  },
  methods: {
    onClick() {
      this.$emit('button-click')
    },
  },
}
</script>

<style></style>

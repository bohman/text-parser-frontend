<template>
  <p class="error">{{ text }}</p>
</template>

<script>
export default {
  name: 'Error',
  props: [
    'text',
  ]
}
</script>

<style lang="scss">
@import '../styles/components/error';
</style>

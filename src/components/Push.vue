<template>
  <div class="push">
    <p class="push--large">{{ large }}</p>
    <p class="push--small">{{ small }}</p>
  </div>
</template>

<script>
export default {
  name: 'Push',
  props: [
    'large',
    'small'
  ]
}
</script>

<style lang="scss">
@import '../styles/components/push';
</style>

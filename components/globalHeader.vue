<template lang="html">
  <header class="header">
    <nuxt-link :to="data.link">
      <button class="button__link" type="button" name="button">{{ data.text }}</button>
    </nuxt-link>
  </header>
</template>

<script>
export default {
  props: ['data'],
}
</script>

<style lang="css" scoped>
.header {
  padding: 16px 8vw;
}
</style>

<template lang="html">
  <header class="header">
    <button class="button__link" v-if="isOrigin" @click="keepScroll()" type="button" name="button">{{ data.text }}</button>
    <nuxt-link v-else :to="data.link">
      <button class="button__link" type="button" name="button">{{ data.text }}</button>
    </nuxt-link>
  </header>
</template>

<script>
export default {
  props: ['data'],
  computed: {
    isOrigin: function() {
      let metaTarget = document.querySelector('meta[cm-order="keepscroll"]')

      if (metaTarget) {
        return true;
      }
      else {
        return false
      }
    }
  },
  methods: {
    keepScroll() {
      history.back();
    }
  },
}
</script>

<style lang="css" scoped>
.header {
  padding: 16px 8vw;
}
</style>

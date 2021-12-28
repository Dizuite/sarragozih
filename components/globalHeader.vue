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
  data() {
    return {
    }
  },
  computed: {
    isOrigin: function() {
      if (document.querySelector('meta[cm-order="keepscroll"]')) {
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
  }
}
</script>

<style lang="css" scoped>
.header {
  width: calc(100% - 16vw);
  padding: 16px 8vw;
  background: linear-gradient(rgba(255, 255, 255, 1), rgba(255, 255, 255, 0));
}
</style>

<template lang="html">
  <main class="about-me">
    <global-header class="about-me__header" :data="{text: 'Back', link: '/'}"/>
  </main>
</template>

<script>
export default {
}
</script>

<style lang="css" scoped>
.about-me {
  position: relative;
}

.about-me__header {
  position: fixed;
}
</style>

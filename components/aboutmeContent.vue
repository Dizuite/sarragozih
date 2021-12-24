<template lang="html">
  <main class="aboutme-content">
    <div class="aboutme-content__bloc-image">

    </div>
  </main>
</template>

<script>
export default {
  props: ['data'],
}
</script>

<style lang="css" scoped>
.aboutme-content {
  padding: 64px 8vw;
}

.aboutme-content__bloc-image {
  height: 256px;
  width: 256px;
  background-position: center;
  background-size: cover;
  background-color: lightgrey;
}
</style>

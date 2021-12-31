<template lang="html">
  <section class="viewer" @click="$parent.showViewer = false">
    <img class="viewer__image" v-if="data.url" :src="data.url" alt="">
    <p class="viewer__bloc-text">
      <strong class="typography__white-high" v-if="data.title">{{data.title}}</strong>
      <span class="typography__white-low" v-if="data.dimensions">{{data.dimensions}}</span>
      <span class="typography__white-low" v-if="data.mediumSupport">{{data.mediumSupport}}</span>
    </p>
  </section>
</template>

<script>
export default {
  props: ['data'],
}
</script>

<style lang="css" scoped>
.viewer {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  background-color: rgba(0, 0, 0, .6);
  z-index: var(--top-high);
  cursor: pointer;
  justify-content: flex-end;
  box-sizing: border-box;
  padding: 2vh;
  gap: 32px;
}

.viewer__image {
  max-height: 100%;
  max-width: 100%;
}

.viewer__bloc-text {
  display: flex;
  flex-direction: column;
  width: 30%;
}

@media screen and (max-width: 768px) {
  .viewer {
    flex-direction: column;
    justify-content: center;
  }

  .viewer__bloc-text {
    text-align: center;
    width: 100%;
  }
}
</style>

<template lang="html">
  <main class="overlay" @click="$parent.showOverlay = false">
    <div class="overlay__container">
      <div class="overlay_bloc-image">
        <img class="overlay__image" v-if="data.url" :src="data.url" alt="">
      </div>
      <div class="overlay__bloc-text">
        <span class="typography__white-high" v-if="data.title">{{data.title}}</span>
        <span class="typography__white-low" v-if="data.dimensions">{{data.dimensions}}</span>
        <span class="typography__white-low" v-if="data.mediumSupport">{{data.mediumSupport}}</span>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  props: ['data'],
  mounted() {
    document.querySelector('body').style.overflowY = "hidden";
  },
  beforeDestroy() {
    document.querySelector('body').style.overflowY = "scroll";
  }
}
</script>

<style lang="css" scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  background-color: rgba(0, 0, 0, .6);
  z-index: var(--top-high);
  cursor: pointer;
}

.overlay__container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 84%;
  height: 80%;
  margin-left: 8%;
}

.overlay_bloc-image {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  width: calc(70% - 32px);
  height: 100%;
  max-width: calc(70% - 32px);
  max-height: 100%;
  margin-right: 32px;
}

.overlay__image {
  max-height: 100%;
  max-width: 100%;
}

.overlay__bloc-text {
  display: flex;
  flex-direction: column;
  width: 30%;
}
</style>

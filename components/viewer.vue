<template lang="html">
  <main class="viewer" @click="$parent.showViewer = false">
    <div class="viewer__container">
      <div class="viewer_bloc-image">
        <img class="viewer__image" v-if="data.url" :src="data.url" alt="">
      </div>
      <div class="viewer__bloc-text">
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
.viewer {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  min-height: 100vh;
  display: flex;
  align-items: center;
  background-color: rgba(0, 0, 0, .6);
  overflow-y: scroll;
  z-index: var(--top-high);
  cursor: pointer;
}

.viewer__container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 84%;
  height: 80%;
  margin-left: 8%;
}

.viewer_bloc-image {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  width: calc(70% - 32px);
  height: 100%;
  max-width: calc(70% - 32px);
  max-height: 100%;
  margin-right: 32px;
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
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    background-color: rgba(0, 0, 0, .6);
    z-index: var(--top-high);
    cursor: pointer;
  }

  .viewer__container {
    display: flex;
    flex-wrap: wrap;
    justify-content: initial;
    align-items: initial;
    width: 84%;
    height: initial;
    margin: 0;
    padding: 32px 8%;
  }

  .viewer_bloc-image {
    display: initial;
    justify-content: initial;
    align-items: initial;
    text-align: center;
    width: 100%;
    max-width: 100%;
    max-height: 100%;
    margin-right: 0;
  }

  .viewer__image {
    max-height: 64vh;
    max-width: 100%;
  }

  .viewer__bloc-text {
    align-items: center;
    width: 100%;
    margin-top: 16px;
    text-align: center;
  }
}
</style>

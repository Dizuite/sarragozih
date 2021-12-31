<template lang="html">
  <main class="landing" :style="cssVars">
    <a class="landing__button-arrow-down button__button-border" href="#content">
      <Arrow class="landing__arrow-down" />
      View more
    </a>
  </main>
</template>

<script>
import Arrow from "~/static/icons/arrow_down.svg?inline";

export default {
  components: { Arrow },
  props: ['src'],
  computed: {
      cssVars () {
        return{
          '--image-src': `url(${this.src})`,
        }
    }
  }
}
</script>

<style lang="css" scoped>
.landing {
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  padding: 32px 8vw;
  background-image: var(--image-src);
  background-position: center;
  background-size: cover;
  background-color: lightgrey;
  box-sizing: border-box;
  height: 100vh;
}

.landing__button-arrow-down {
  display: flex;
  justify-content: space-between;
  align-items: center;
  text-decoration: none;
  gap: 6px;
}

.landing__arrow-down {
  width: 1.5em;
  fill: currentColor;
}
</style>

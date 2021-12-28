<template lang="html">
  <main class="landing" :style="{backgroundImage: `url(${data})`, height: height}">
    <div>
      <button class="landing__button-arrow-down button__button-border" @click="scroll()" type="button" name="button">
        <img class="landing__arrow-down" src="icons/arrow_down.svg" alt="Arrow pointing dow">
        <span class="typography__button">View more</span>
      </button>
    </div>
  </main>
</template>

<script>
export default {
  props: ['data'],
  data() {
    return {
      height: `${window.innerHeight - 64}px`
    };
  },
  methods: {
    scroll() {
      this.$parent.scroll();
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
  background-position: center;
  background-size: cover;
  background-color: lightgrey;
}

.landing__button-arrow-down {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.landing__arrow-down {
  width: 20px;
  margin-right: 6px;
  filter: invert(100%);
}
</style>

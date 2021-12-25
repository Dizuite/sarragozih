<template lang="html">
  <main class="aboutme-content">
    <div class="aboutme-content__bloc-image">
      <div class="aboutme-content__image" :style="{backgroundImage: `url(${data.imageLeft})`}"></div>
      <p class="typography__paragraph aboutme-content__paragraph">{{ data.firstText }}</p>
      <div class="aboutme-content__image" :style="{backgroundImage: `url(${data.imageRight})`}"></div>
    </div>
    <div class="aboutme-content__bloc-paragraph">
      <p class="typography__paragraph aboutme-content__paragraph">{{ data.firstText }}</p>
      <p class="typography__paragraph aboutme-content__paragraph">{{ data.secondText }}</p>
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
  display: flex;
  justify-content: space-between;
  padding: 0 8vw;
  margin-bottom: 64px;
}

.aboutme-content__image {
  height: 32vw;
  width: 32vw;
  background-position: center;
  background-size: cover;
  background-color: lightgrey;
}

.aboutme-content__bloc-image > .aboutme-content__paragraph {
  display: none;
}

.aboutme-content__bloc-paragraph {
  padding: 0 8vw;
}

@media screen and (max-width: 768px) {
  .aboutme-content__bloc-image {
    flex-wrap: wrap;
    padding: 0;
    margin-bottom: 0;
  }

  .aboutme-content__image {
    height: 86vw;
    width: 86vw;
    background-position: center;
    background-size: cover;
    background-color: lightgrey;
    margin-bottom: 8vw;
  }

  .aboutme-content__bloc-paragraph {
    padding: 0;
  }

  .aboutme-content__paragraph {
    margin-bottom: 8vw;
  }

  .aboutme-content__bloc-image > .aboutme-content__paragraph {
    display: initial;
  }

  .aboutme-content__paragraph:first-child {
    display: none;
  }
}
</style>

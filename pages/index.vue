<template>
  <main class="main">
    <landing :data="landingBackground" />
    <div :class="{'main__header-sticky': isSticky}">
      <global-header :data="{text: 'About', link: '/aboutme'}"/>
    </div>
    <div class="main__header-replace-zone" v-if="isSticky"></div>
    <gallery v-if="storyContentGallery.length > 0" :data="{galleryData: storyContentGallery}" />
    <global-footer class=""/>
    <transition name="fade">
      <viewer v-if="showViewer" :data="{url: imageUrl, title: imageTitle, dimensions: imageDimensions, mediumSupport: imageMediumSupport}" />
    </transition>
  </main>
</template>

<script>
export default {
  head: {
    meta: [{'cm-order': 'keepscroll'}],
  },
  async asyncData(context) {
    let storyContent;
    let landingBackground;

    storyContent = await context.app.$storyapi.get('cdn/stories/home_page', {}).then((res) => {
      return res.data.story.content;
    }).catch((res) => {
      if (!res.response) {
        console.error(res);
        context.error({ statusCode: 404, message: 'Failed to receive content form api' });
      }
      else {
        console.error(res.response.data);
        context.error({ statusCode: res.response.status, message: res.response.data });
      }
    });
    landingBackground = storyContent.landing_background.filename;

    return {
      landingBackground: landingBackground,
      storyContentGallery: storyContent.gallery,
    };
  },
  data() {
    return {
      isSticky: false,
      widthHeader: 'calc(100% - 8vw)',
      showViewer: false,
      imageUrl: '',
      imageTitle: '',
      imageDimensions: '',
      imageMediumSupport: '',
    }
  },
  methods: {
    monitorHeader() {
      let position = (document.body.getBoundingClientRect().top * -1);
      let limit = window.innerHeight;

      if (position > limit) {
        this.isSticky = true;
      }
      else {
        this.isSticky = false;
      }
    },
    async scroll() {
      let landingHeight = window.innerHeight;

      window.scrollTo({
        top: landingHeight,
        behavior: 'smooth'
      });
    },
  },
  mounted() {
    window.addEventListener('scroll', this.monitorHeader, {passive: true});
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.monitorHeader);
  }
}
</script>

<style lang="css" scoped>
.main {
  position: relative;
}

.main__header-sticky {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: var(--high);
  transition: .1s;
}

.main__header-replace-zone {
  height: 54px;
}
</style>

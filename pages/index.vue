<template>
  <main class="main">
    <landing :data="landingBackground" />
    <div :class="{'main__header-paused' : true, 'main__header-sticky': isSticky }">
      <global-header :data="{text: 'About', link: '/about-me'}"/>
    </div>
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

    storyContent = await context.app.$storyapi.get(`cdn/stories/home_page`, {}).then((res) => {
      return res.data.story.content;
    }).catch((res) => {
      if (!res.response) {
        console.error(res)
        context.error({ statusCode: 404, message: 'Failed to receive content form api' })
      } else {
        console.error(res.response.data)
        context.error({ statusCode: res.response.status, message: res.response.data })
      }
    });
    landingBackground = storyContent.landing_background.filename;
    return {
      landingBackground: landingBackground,
    };
  },
  data() {
    return {
      isSticky: false,
    }
  },
  methods: {
    monitorHeader() {
      let position = (document.body.getBoundingClientRect().top * -1)
      let limit = window.innerHeight

      if (position > limit) {
        this.isSticky = true;
      }
      else {
        this.isSticky = false;
      }
    },
    launchHeader() {
      window.addEventListener('scroll', this.monitorHeader, {passive: true})
    },
    async scroll() {
      let landingHeight = window.innerHeight;

      // if (landingHeight < 585) // petits écrans
      //   landingHeight = 585
      // else if (landingHeight > 1050) // grands écrans
      //   landingHeight = 1050
      window.scrollTo({
        top: landingHeight,
        behavior: 'smooth'
      });
    }
  },
  mounted() {
    this.launchHeader();
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.monitorHeader)
  }
}
</script>

<style lang="css" scoped>
.main {
  position: relative;
}

.main__header-paused {

}

.main__header-sticky {
  position: fixed;
  top: 0;
  left: 0;
}
</style>

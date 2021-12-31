<template lang="html">
  <main class="about-me">
    <global-header class="about-me__header" :data="{text: 'Back', link: '/'}"/>
    <aboutme-content :data="{imageLeft: imageLeft, imageRight: imageRight, firstText: firstText, secondText: secondText}" />
    <global-footer/>
  </main>
</template>

<script>
export default {
  async asyncData(context) {
    const { image_left, image_right, text_1, text_2 } = await context.app.$storyapi.get('cdn/stories/about_me', {}).then((res) => {
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

    return {
      imageLeft: image_left.filename,
      imageRight: image_right.filename,
      firstText: text_1.content[0].content[0].text,
      secondText: text_2.content[0].content[0].text
    };
  },
}
</script>

<style lang="css" scoped>
.about-me__header {
  position: fixed;
}
</style>

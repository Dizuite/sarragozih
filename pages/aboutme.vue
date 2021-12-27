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
    let storyContent;
    let imageLeft;
    let imageRight;
    let firstText;
    let secondText;

    storyContent = await context.app.$storyapi.get(`cdn/stories/about_me`, {}).then((res) => {
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

    imageLeft = storyContent.image_left.filename;
    imageRight = storyContent.image_right.filename;
    firstText = storyContent.text_1.content[0].content[0].text;
    secondText = storyContent.text_2.content[0].content[0].text;

    return {
      imageLeft: imageLeft,
      imageRight: imageRight,
      firstText: firstText,
      secondText: secondText
    };
  },
}
</script>

<style lang="css" scoped>
.about-me {
  position: relative;
}

.about-me__header {
  position: fixed;
}
</style>

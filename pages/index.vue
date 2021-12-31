<template>
  <main class="main">
    <landing :src="landingImage" />
    <global-header class="main__header-sticky" :data="{text: 'About', link: '/aboutme'}"/>
    <gallery id="content" v-if="images.length" :images="images" />
    <global-footer/>
    <transition name="fade">
      <viewer v-if="showViewer" :data="{url: imageUrl, title: imageTitle, dimensions: imageDimensions, mediumSupport: imageMediumSupport}" />
    </transition>
  </main>
</template>

<script>
export default {
  async asyncData(context) {
    // const { landing_background, gallery } = await context.app.$storyapi.get('cdn/stories/home_page', {}).then((res) => {
    //   return res.data.story.content;
    // }).catch((res) => {
    //   if (!res.response) {
    //     console.error(res);
    //     context.error({ statusCode: 404, message: 'Failed to receive content form api' });
    //   }
    //   else {
    //     console.error(res.response.data);
    //     context.error({ statusCode: res.response.status, message: res.response.data });
    //   }
    // });
    const { landing_background, gallery } = {
    "_uid": "22832a69-0f77-49c8-be43-88a4d545682f",
    "gallery": [
        {
            "img": {
                "id": 3570633,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/1080x1350/aeebb2385d/arret_du_temps.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "ca3bc639-6236-4ffb-a3a6-7d737f7a7f76",
            "title": "Arrêt du temps",
            "component": "painting",
            "dimensions": "Format A3",
            "medium_support": "Bic sur papier"
        },
        {
            "img": {
                "id": 3570634,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/1080x1080/987840bc6f/crepuscule.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "619d3d7d-eead-4340-99b7-c493b1357789",
            "title": "Crépuscule",
            "component": "painting",
            "dimensions": "30x40cm",
            "medium_support": "Acrylique sur coton"
        },
        {
            "img": {
                "id": 3570636,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/1080x739/0f34f1f51d/chateau_dans_le_ciel.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "0b37562e-46cc-4f8d-b838-49d3ae6ad2ee",
            "title": "Château dans le ciel",
            "component": "painting",
            "dimensions": "75x115cm",
            "medium_support": "Acrylique sur toile"
        },
        {
            "img": {
                "id": 3570637,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/1080x1350/32840397a3/vue_sur_toits.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "97a7e812-00c0-460e-b96f-9df4a7702e8e",
            "title": "Vue sur toits",
            "component": "painting",
            "dimensions": "",
            "medium_support": ""
        },
        {
            "img": {
                "id": 3570638,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/760x760/a7797f7f52/vue_sur_lac.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "0b3cca21-fda6-414b-8c9e-6b44986c460a",
            "title": "Vue sur lac",
            "component": "painting",
            "dimensions": "40x40cm",
            "medium_support": "Acrylique sur coton"
        },
        {
            "img": {
                "id": 3570639,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/1080x1080/73d3817c13/bouffee_d_oxygene.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "f2dad78d-5b3b-4fad-89f7-34a69c58d874",
            "title": "Bouffée d'oxygène",
            "component": "painting",
            "dimensions": "",
            "medium_support": ""
        },
        {
            "img": {
                "id": 3570640,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/1080x1080/caa96cb13c/abstraction_industrielle.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "b7b92ed5-0966-4f2b-b21b-1918d78e0e56",
            "title": "Abstraction industrielle",
            "component": "painting",
            "dimensions": "50x90cm",
            "medium_support": "Acrylique sur coton"
        },
        {
            "img": {
                "id": 3570641,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/1600x1076/bc428db7ec/cambronne.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "1cde6282-5b87-4171-8374-911ee4c80bdf",
            "title": "Cambronne",
            "component": "painting",
            "dimensions": "Format A4",
            "medium_support": "Feutre sur papier"
        },
        {
            "img": {
                "id": 3570642,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/1080x1080/cd9284a443/doux_melange.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "be24d4b7-aaaa-4328-965c-02f4c1043fca",
            "title": "Doux mélange",
            "component": "painting",
            "dimensions": "Format A4",
            "medium_support": "Acrylique et bic sur papier"
        },
        {
            "img": {
                "id": 3570643,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/1080x1350/b9ba377196/temoin.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "febd48bb-2882-43f2-b8fc-6bad24a2dabe",
            "title": "Témoin",
            "component": "painting",
            "dimensions": "Format A5",
            "medium_support": "Bic et feutre sur papier"
        },
        {
            "img": {
                "id": 3570644,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/988x608/8064bceba9/reveur.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "192c7393-82fb-4971-bc9e-27dabf6abb7f",
            "title": "Rêveur",
            "component": "painting",
            "dimensions": "110x75cm",
            "medium_support": "Acrylique sur coton"
        },
        {
            "img": {
                "id": 3570645,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/744x930/52647ba2c1/mepris.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "c4067053-bee5-4783-9e29-f9a5637c8314",
            "title": "Mépris",
            "component": "painting",
            "dimensions": "Format A5",
            "medium_support": "Feutre sur papier"
        },
        {
            "img": {
                "id": 3570646,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/793x793/277d9d6afd/mutations.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "3bbf58f5-77a6-43fb-bc2b-8612d1d1e7b4",
            "title": "Mutations",
            "component": "painting",
            "dimensions": "Format A5",
            "medium_support": "Feutre sur papier"
        },
        {
            "img": {
                "id": 3570647,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/789x789/078990d3c5/mutations2.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "33e413f8-4eab-478a-a208-dfc26bee5fa3",
            "title": "Mutations 2",
            "component": "painting",
            "dimensions": "Format A5",
            "medium_support": "Feutre sur papier"
        },
        {
            "img": {
                "id": 3570648,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/4255x2985/9131505ac9/ombre_sur_pont.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "0392c795-379f-4564-b8a0-cc00ce22663a",
            "title": "Ombre sur pont",
            "component": "painting",
            "dimensions": "Format A5",
            "medium_support": "Bic sur papier"
        },
        {
            "img": {
                "id": 3570649,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/1080x1080/733d9043c0/tbm.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "80f86db1-1baa-4f95-ae21-c6801a6c273e",
            "title": "TBM",
            "component": "painting",
            "dimensions": "Format A4",
            "medium_support": "Acrylique, bic et crayons de couleurs sur papier"
        },
        {
            "img": {
                "id": 3570650,
                "alt": "",
                "name": "",
                "focus": null,
                "title": "",
                "filename": "https://a.storyblok.com/f/140482/3120x3900/62a8b4d6b4/vieux_pecheur.jpeg",
                "copyright": "",
                "fieldtype": "asset"
            },
            "_uid": "fba9aa11-fa9b-4d80-87ce-142c81e47922",
            "title": "Vieux pêcheur",
            "component": "painting",
            "dimensions": "Format A5",
            "medium_support": "Mine de plomb sur papier"
        }
    ],
    "component": "page_home_page",
    "landing_background": {
        "id": 3568040,
        "alt": "",
        "name": "",
        "focus": null,
        "title": "",
        "filename": "https://a.storyblok.com/f/140482/988x608/f4253403aa/reveur.jpeg",
        "copyright": "",
        "fieldtype": "asset"
    }
}

    return {
      landingImage: landing_background.filename,
      images: gallery,
    };
  },
  data() {
    return {
      showViewer: false,
      imageUrl: '',
      imageTitle: '',
      imageDimensions: '',
      imageMediumSupport: '',
    }
  },
}
</script>

<style lang="css" scoped>
.main__header-sticky {
  position: sticky;
  top: 0;
  left: 0;
  z-index: var(--high);
}
</style>

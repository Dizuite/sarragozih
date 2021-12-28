<template lang="html">
  <main class="gallery">
    <div class="gallery__column-desktop gallery__column-left">
      <div class="gallery__image-bloc"
           v-for="(item, index) in data.galleryData"
           v-if="item.totalGcdNow <= totalGcd / 3"
           :key="`${index}-col-1`">
        <div class="gallery__image-overlay" @click="openViewer(item.title, item.img.filename, item.dimensions, item.medium_support)">
          <span class="typography__white-regular" v-if="item.title != ''">{{item.title}}</span>
          <span class="typography__white-low" v-if="item.dimensions != ''">{{item.dimensions}}</span>
          <span class="typography__white-low" v-if="item.medium_support != ''">{{item.medium_support}}</span>
        </div>
        <img class="gallery__image" :src="item.img.filename" alt="">
      </div>
    </div>
    <div class="gallery__column-desktop gallery__column-center">
      <div class="gallery__image-bloc"
           v-for="(item, index) in data.galleryData"
           v-if="item.totalGcdNow > totalGcd / 3 && item.totalGcdNow < (totalGcd / 3) * 2"
           :key="`${index}-col-2`">
        <div class="gallery__image-overlay" @click="openViewer(item.title, item.img.filename, item.dimensions, item.medium_support)">
          <span class="typography__white-regular" v-if="item.title != ''">{{item.title}}</span>
          <span class="typography__white-low" v-if="item.dimensions != ''">{{item.dimensions}}</span>
          <span class="typography__white-low" v-if="item.medium_support != ''">{{item.medium_support}}</span>
        </div>
        <img class="gallery__image" :src="item.img.filename" alt="">
      </div>
    </div>
    <div class="gallery__column-desktop gallery__column-right">
      <div class="gallery__image-bloc"
           v-for="(item, index) in data.galleryData"
           v-if="item.totalGcdNow >= (totalGcd / 3) * 2"
           :key="`${index}-col-3`">
        <div class="gallery__image-overlay" @click="openViewer(item.title, item.img.filename, item.dimensions, item.medium_support)">
          <span class="typography__white-regular" v-if="item.title != ''">{{item.title}}</span>
          <span class="typography__white-low" v-if="item.dimensions != ''">{{item.dimensions}}</span>
          <span class="typography__white-low" v-if="item.medium_support != ''">{{item.medium_support}}</span>
        </div>
        <img class="gallery__image" :src="item.img.filename" alt="">
      </div>
    </div>
    <div class="gallery__column-mobile">
      <div class="gallery__image-bloc"
           v-for="(item, index) in data.galleryData"
           v-if="item.totalGcdNow <= totalGcd / 2"
           :key="`${index}-col-1`">
        <img class="gallery__image-mobile" @click="openViewer(item.title, item.img.filename, item.dimensions, item.medium_support)" :src="item.img.filename" alt="">
      </div>
    </div>
    <div class="gallery__column-mobile">
      <div class="gallery__image-bloc-mobile"
           v-for="(item, index) in data.galleryData"
           v-if="item.totalGcdNow > totalGcd / 2"
           :key="`${index}-col-2`">
        <img class="gallery__image-mobile" @click="openViewer(item.title, item.img.filename, item.dimensions, item.medium_support)" :src="item.img.filename" alt="">
      </div>
    </div>
  </main>
</template>

<script>
export default {
  props: ['data'],
  data() {
    return {
      totalGcd: 0,
    }
  },
  methods: {
    getGcd(w, h) {
      return (h == 0) ? w : this.getGcd(h, w % h);
    },
    openViewer(title, img, dimensions, mediumSupport) {
      this.$parent.imageTitle = title ? title : 'Pas de titre';
      this.$parent.imageUrl = img ? img : false;
      this.$parent.imageDimensions = dimensions ? dimensions : 'Pas de dimensions';
      this.$parent.imageMediumSupport = mediumSupport ? mediumSupport : false;
      this.$parent.showOverlay = true;
    }
  },
  mounted() {
    let self = this;

    for (let i = 0; i < this.data.galleryData.length; i++) {
      let img = new Image();

      img.src = this.data.galleryData[i].img.filename;
      img.onload = function() {
        let totalGcdNow = self.totalGcd;
        let w = this.width;
        let h = this.height;
        let r = self.getGcd(w, h);

        self.data.galleryData[i]['gcd'] = r;
        self.data.galleryData[i]['ratio'] = (w / r) - (h / r);
        self.data.galleryData[i]['totalGcdNow'] = totalGcdNow + r;
        self.totalGcd += r;
      }
    }
  }
}
</script>

<style lang="css" scoped>
.gallery {
  display: flex;
  justify-content: center;
  margin: 32px 8vw;
  padding: 8px;
  background-color: var(--tertiary-color);
}

.gallery__column-desktop {
  display: flex;
  flex-direction: column;
}

.gallery__column-left .gallery__image {
  width: calc(28vw - 11px);
}

.gallery__column-center {
  margin: 0 8px;
}

.gallery__column-center .gallery__image {
  width: calc(28vw - 10px);
}

.gallery__column-right .gallery__image {
  width: calc(28vw - 11px);
}

.gallery__image-bloc {
  position: relative;
  display: flex;
  padding-bottom: 8px;
  cursor: pointer;
}

.gallery__image-bloc:nth-last-child(1) {
  padding-bottom: 0px;
}

.gallery__image-bloc:nth-last-child(1) .gallery__image-overlay {
  height: calc(100% - 16px);
}

.gallery__image-overlay {
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  top: 0;
  left: 0;
  width: calc(100% - 16px);
  height: calc(100% - 24px);
  padding: 8px;
  background-color: rgba(0, 0, 0, 0);
  opacity: 0;
  z-index: var(--regular-high);
  transition: .2s;
}

.gallery__image-overlay:hover {
  background-color: rgba(0, 0, 0, .4);
  opacity: 1;
}

.gallery__image {
  width: calc(28vw - 8px);
}

.gallery__column-mobile {
  display: none;
  flex-direction: column;
}

.gallery__image-bloc-mobile {
  display: flex;
  padding-bottom: 8px;
}

.gallery__image-bloc-mobile:nth-last-child(1) {
  padding-bottom: 0px;
}


.gallery__image-mobile {
  width: calc(42vw - 12px);
}

@media screen and (max-width: 768px) {
  .gallery {
    margin: 16px 8vw;
    padding: 8px;
    justify-content: space-between;
  }

  .gallery__column-desktop {
    display: none;
  }

  .gallery__column-mobile {
    display: flex;
  }

  .gallery__image-mobile {
    width: calc(42vw - 12px);
  }
}
</style>

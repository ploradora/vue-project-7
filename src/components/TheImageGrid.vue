<template>
  <div class="gallery-container">
    <div class="images">
      <the-slider-mobile></the-slider-mobile>
      <div
        class="images-grid-view"
        v-for="(image, index) in mainImages"
        :key="index"
      >
        <img
          @click="openModalGallery(index)"
          class="main-image"
          v-if="currentTab === image.imgNumber"
          :src="image.img"
          :alt="image.alt"
        />
      </div>
      <div
        class="thumbnail-container"
        :class="{ activeThumbnail: currentTab === thumbnail.imgNumber }"
        v-for="(thumbnail, index) in thumbnails"
        :key="index"
        @click="selectTab(thumbnail.imgNumber)"
      >
        <img class="thumbnail" :src="thumbnail.img" :alt="thumbnail.alt" />
      </div>
    </div>
  </div>
  <teleport to="body">
    <the-slider
      class="the-slider"
      @close-modal="closeModal"
      v-if="modalState"
      :modal="this.modalState"
      :current-tab="currentTab"
    ></the-slider>
  </teleport>
</template>

<script>
import TheSlider from "../components/slider-desktop-modal/TheSlider.vue";
import TheSliderMobile from "./mobile-slider/TheSliderMobile.vue";
export default {
  components: {
    TheSlider,
    TheSliderMobile,
  },
  data() {
    return {
      mainImages: [
        {
          img: require("../assets/images/image-product-1.jpg"),
          alt: "leather shoes",
          imgNumber: 0,
        },
        {
          img: require("../assets/images/image-product-2.jpg"),
          alt: "2 white rocks, a pair of shoes on display and a dried out branch",
          imgNumber: 1,
        },
        {
          img: require("../assets/images/image-product-3.jpg"),
          alt: "one shoe on the top of 2 white rocks",
          imgNumber: 2,
        },
        {
          img: require("../assets/images/image-product-4.jpg"),
          alt: "one shoe on the top of 2 white rocks",
          imgNumber: 3,
        },
      ],
      thumbnails: [
        {
          img: require("../assets/images/image-product-1-thumbnail.jpg"),
          alt: "leather shoes",
          imgNumber: 0,
        },
        {
          img: require("../assets/images/image-product-2-thumbnail.jpg"),
          alt: "2 white rocks, a pair of shoes on display and a dried out branch",
          imgNumber: 1,
        },
        {
          img: require("../assets/images/image-product-3-thumbnail.jpg"),
          alt: "one shoe on the top of 2 white rocks",
          imgNumber: 2,
        },
        {
          img: require("../assets/images/image-product-4-thumbnail.jpg"),
          alt: "one shoe on the top of 2 white rocks",
          imgNumber: 3,
        },
      ],
      currentSlide: 0,
      currentTab: 0,
      modalState: false,
    };
  },
  mounted() {
    this.cancelModalImage();
    window.addEventListener("resize", this.cancelModalImage);
  },
  methods: {
    closeModal(state) {
      this.modalState = state;
    },
    openModalGallery() {
      this.modalState = true;
      document.body.style.overflow = "hidden";
      this.cancelModalImage();
    //   console.log(this.currentTab);
    },
    selectTab(tab) {
      this.currentTab = tab;
    },
    cancelModalImage() {
      const ignoreClick = window.innerWidth;
      if (ignoreClick < 1000) {
        this.modalState = false;
        document.body.style.overflow = "unset";
      }
    },
  },
};
</script>

<style scoped lang="scss">
@mixin grid-enter {
  @media only screen and(min-width: 502px) {
    @content;
  }
}
@mixin tablet {
  @media only screen and(min-width: 851px) {
    @content;
  }
}
@mixin desktop {
  @media only screen and(min-width: 1000px) {
    @content;
  }
}

.gallery-container {
  width: 100%;
  position: relative;
  .images {
    .images-grid-view {
      display: none;
    }
    .mobile-slider {
      display: flex;
      overflow: hidden;
      width: 100%;
      max-height: 500px;
      img {
        object-fit: cover;
        object-position: center;
        width: 100%;
        display: block;
      }
    }
    .thumbnail {
      display: none;
    }
  }
  @include grid-enter {
    width: 90%;
    max-width: 452.15px;
    margin: auto;
    margin-top: 50px;
    margin-bottom: 60px;
    .images {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(90px, 1fr));
      grid-template-rows: 452.15px 1fr;
      gap: 18px;
      max-width: 499px;
      margin: auto;
      .mobile-slider {
        display: none;
      }
      .images-grid-view {
        position: absolute;
        display: block;
        grid-column: 1 / -1;
        .main-image {
          width: 100%;
          border-radius: 15px;
        }
      }
      .thumbnail-container {
        position: relative;
        user-select: none;
        cursor: pointer;
        grid-row: 2 / 3;
        &:hover {
          &::after {
            position: absolute;
            content: "";
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(255, 255, 255, 0.555);
            border-radius: 10px;
          }
        }
        .thumbnail {
          display: block;
          width: 100%;
          border-radius: 10px;
        }
      }
      .activeThumbnail {
        position: relative;
        &::after {
          position: absolute;
          content: "";
          top: 0;
          bottom: 0;
          left: 0;
          right: 0;
          width: 100%;
          height: 100%;
          border-radius: 10px;
          background-color: rgba(255, 255, 255, 0.555);
          border: 3px solid hsl(26, 100%, 55%);
        }
        &:hover {
          background-color: rgba(255, 255, 255, 0.555);
        }
      }
    }
  }
  @include desktop {
    max-width: 400px;
    margin: unset;
    .images {
      grid-template-columns: repeat(auto-fit, minmax(86px, 1fr));
      grid-template-rows: 400px 1fr;
      .images-grid-view {
        .main-image {
          cursor: pointer;
        }
      }
    }
  }
}
.the-slider {
  display: none;
  @include desktop {
    display: unset;
  }
}
</style>

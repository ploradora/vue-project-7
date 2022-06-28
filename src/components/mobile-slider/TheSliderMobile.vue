<template>
  <div class="slider-container-mobile">
    <slider-control-mobile
      @switch="switchDirection($event)"
      @prev="prev"
      @next="next"
    ></slider-control-mobile>
    <div class="slider-item-mobile">
      <slider-item-mobile
        v-for="(image, index) in mainImages"
        :key="index"
        :image="image"
        :index="index"
        :current-slide="currentSlide"
        :direction="direction"
      ></slider-item-mobile>
    </div>
  </div>
</template>

<script>
import SliderItemMobile from "./SliderItemMobile.vue";
import SliderControlMobile from "./SliderControlMobile.vue";
export default {
  components: {
    SliderItemMobile,
    SliderControlMobile,
  },
  data() {
    return {
      mainImages: [
        {
          img: require("../../assets/images/image-product-1.jpg"),
          alt: "leather shoes",
          imgNumber: 0,
        },
        {
          img: require("../../assets/images/image-product-2.jpg"),
          alt: "2 white rocks, a pair of shoes on display and a dried out branch",
          imgNumber: 1,
        },
        {
          img: require("../../assets/images/image-product-3.jpg"),
          alt: "one shoe on the top of 2 white rocks",
          imgNumber: 2,
        },
        {
          img: require("../../assets/images/image-product-4.jpg"),
          alt: "one shoe on the top of 2 white rocks",
          imgNumber: 3,
        },
      ],
      currentSlide: 0,
      direction: "right",
    };
  },
  methods: {
    prev(step = -1) {
      const index =
        this.currentSlide > 0
          ? this.currentSlide + step
          : this.mainImages.length - 1;
      this.setCurrentSlide(index);
      this.direction = "left";
    },
    next(step = 1) {
      const index =
        this.currentSlide < this.mainImages.length - 1
          ? this.currentSlide + step
          : 0;
      this.setCurrentSlide(index);
      this.direction = "right";
    },
    setCurrentSlide(index) {
      this.currentSlide = index;
    },
    switchSlide(index) {
      const step = index - this.currentSlide;
      if (step > 0) {
        this.next(step);
      } else {
        this.prev(step);
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
.slider-container-mobile {
  width: 100%;
  max-width: 501px;
  height: 380px;
  .slider-item-mobile {
    position: absolute;
    overflow: hidden;
    width: 100%;
    height: 100%;
  }
  @include grid-enter {
    display: none;
  }
}
</style>

<template>
  <div class="slider-parent">
    <div class="overlay" @click="closeModal"></div>
    <div class="slider-container">
      <svg
        @click="closeModal"
        class="icon-close"
        width="14"
        height="15"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="m11.596.782 2.122 2.122L9.12 7.499l4.597 4.597-2.122 2.122L7 9.62l-4.595 4.597-2.122-2.122L4.878 7.5.282 2.904 2.404.782l4.595 4.596L11.596.782Z"
          fill="#69707D"
          fill-rule="evenodd"
        />
      </svg>
      <slider-controls
        :current-index="currentSlide"
        @switch="switchSlide($event)"
        @prev="prev"
        @next="next"
      ></slider-controls>
      <div class="slider-inner">
        <slider-item
          v-for="(slide, index) in slidesArray"
          :key="index"
          :slide="slide"
          :current-slide="currentSlide"
          :index="index"
          :direction="direction"
        ></slider-item>
      </div>
    </div>
  </div>
</template>

<script>
import SliderItem from "./SliderItem.vue";
import SliderControls from "./SliderControls.vue";
export default {
  components: {
    SliderItem,
    SliderControls,
  },
  props: ["modal", "currentTab"],
  emits: ["close-modal"],

  data() {
    return {
      slidesArray: [
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

      overlay: false,
      currentSlide: 0,
      direction: "right",
    };
  },
  beforeMount() {
    this.currentSlide = this.currentTab;
  },
  methods: {
    prev(step = -1) {
      const index =
        this.currentSlide > 0
          ? this.currentSlide + step
          : this.slidesArray.length - 1;
      this.setCurrentSlide(index);
      this.direction = "left";
    },
    next(step = 1) {
      const index =
        this.currentSlide < this.slidesArray.length - 1
          ? this.currentSlide + step
          : 0;
      this.setCurrentSlide(index);
      this.direction = "right";
    },
    closeModal() {
      this.$emit("close-modal", this.overlay);
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
@media only screen and (min-width: 1000px) {
  .slider-parent {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 20;
    .overlay {
      position: absolute;
      top: 0;
      width: 100%;
      min-height: 100vh;
      background-color: rgba(0, 0, 0, 0.75);
      cursor: pointer;
    }
    .slider-container {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -60%);
      width: 480px;
      height: 480px;
      .icon-close {
        position: absolute;
        right: 0;
        top: -30px;
        cursor: pointer;
        transform: scale(1.15);
        path {
          fill: hsl(223, 64%, 98%);
        }
      }
      .slider-inner {
        width: 100%;
        height: 100%;
        position: relative;
        overflow: hidden;
        border-radius: 15px;
        z-index: 21;
      }
    }
  }
}
</style>

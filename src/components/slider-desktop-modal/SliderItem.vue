<template>
  <transition :name="transitionEffect">
    <div class="slider-item" v-show="currentSlide === index">
      <img class="main-images" :src="slide.img" :alt="slide.alt" />
    </div>
  </transition>
</template>

<script>
export default {
  props: ["slide", "currentSlide", "index", "direction"],
  computed: {
    transitionEffect() {
      return this.direction === "right" ? "slide-out" : "slide-in";
    },
  },
};
</script>

<style scoped lang="scss">
@media only screen and (min-width: 1000px) {
  .slider-item {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    .main-images {
      width: 100%;
      display: block;
    }
  }
  .slide-in-enter-active,
  .slide-in-leave-active,
  .slide-out-enter-active,
  .slide-out-leave-active {
    transition: all 0.2s ease-in-out;
  }
  .slide-in-enter-from {
    transform: translateX(-100%);
  }
  .slide-in-leave-to {
    transform: translateX(100%);
  }
  .slide-out-enter-from {
    transform: translateX(100%);
  }
  .slide-out-leave-to {
    transform: translateX(-100%);
  }
}
</style>

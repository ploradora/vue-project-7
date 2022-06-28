<template>
  <div class="arrows-mobile">
    <div class="left" @click="$emit('prev')">
      <img
        class="icon-left"
        src="../../assets/images/icon-previous.svg"
        alt="icon arrow left"
      />
    </div>
    <div class="right" @click="$emit('next')">
      <img
        class="icon-right"
        src="../../assets/images/icon-next.svg"
        alt="icon arrow right"
      />
    </div>
  </div>
  <div class="thumbnail-controls">
    <div
      class="thumbnail-wrapper"
      :class="{ activeThumbnail: currentIndex === index }"
      v-for="(thumbnail, index) in thumbnails"
      :key="index"
      @click="$emit('switch', index)"
    >
      <img class="thumbnail" :src="thumbnail.img" :alt="thumbnail.alt" />
    </div>
  </div>
</template>

<script>
export default {
  props: ["currentIndex"],
  emits: ["prev", "next", "switch"],
  data() {
    return {
      thumbnails: [
        {
          img: require("../../assets/images/image-product-1-thumbnail.jpg"),
          alt: "leather shoes",
          imgNumber: 0,
        },
        {
          img: require("../../assets/images/image-product-2-thumbnail.jpg"),
          alt: "2 white rocks, a pair of shoes on display and a dried out branch",
          imgNumber: 1,
        },
        {
          img: require("../../assets/images/image-product-3-thumbnail.jpg"),
          alt: "one shoe on the top of 2 white rocks",
          imgNumber: 2,
        },
        {
          img: require("../../assets/images/image-product-4-thumbnail.jpg"),
          alt: "one shoe on the top of 2 white rocks",
          imgNumber: 3,
        },
      ],
      currentThumbnail: 0,
    };
  },
  methods: {
    selectThumbnail(thumbnail) {
      this.currentThumbnail = thumbnail;
    },
  },
};
</script>

<style scoped lang="scss">
@media only screen and (min-width: 1000px) {
  .arrows-mobile {
    width: 521px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: flex;
    align-items: center;
    justify-content: space-between;
    user-select: none;
    z-index: 22;
    .left,
    .right {
      background-color: #fff;
      width: 43px;
      height: 43px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      position: relative;
      cursor: pointer;
      .icon-left {
        left: 47%;
      }
      .icon-right {
        cursor: pointer;
        left: 52%;
      }
      img {
        position: absolute;
        width: 9px;
        display: block;
        top: 50%;
        transform: translate(-50%, -50%);
        pointer-events: none;
      }
    }
  }
  .thumbnail-controls {
    position: absolute;
    bottom: -110px;
    left: 50%;
    width: 400px;
    transform: translateX(-50%);
    display: flex;
    justify-content: space-between;
    z-index: 22;
    .thumbnail-wrapper {
      position: relative;
      user-select: none;
      cursor: pointer;
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
        width: 85px;
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
        border-radius: 10px;
        background-color: rgba(255, 255, 255, 0.555);
      }
    }
  }
}
</style>
